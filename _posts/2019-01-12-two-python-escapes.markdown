---
layout: post
title:  "Kringlecon: Two Python Escapes"
date:   2019-01-12 12:29:29 -0500
categories: 
---

*Warning: this post is a walkthrough and contains spoilers.*

One of the more fun challenges for me in Kringlecon 2018 was the Python escape challenge. You're logged into a restricted Python shell
and had to find some way to execute the file `i_escaped` inside of the user's home directory. Attempting to exit Python via `exit()` would log you
out of the system: you had to find a way to either invoke `bash` or directly run `i_escaped` from inside of Python. This was a practical
exercise to go with Mark Baggett's [https://www.youtube.com/watch?v=ZVx2Sxl3B9c](Escaping Python shells) Kringlecon talk- but at the time I didn't
realize that and dove straight in, which resulted in me finding an alternative solution.

# Escaping the sandbox

Normally running a program from inside Python would just be a few quick commands at the REPL:

```python
import os
os.system("./i_escaped")
```

However, trying to run this immediately blocks you with the message `Use of the command import is prohibited for this question.` One alternative
way we might get around this would be to try to use `exec`, which can take in a string of code and run that. Unfortunately, trying to run `exec`
gives us a similar error message that it's banned as well. Next on our list of tricks is `eval`, which is a little more restricted in what it can run:
it only runs expressions, not statements, but we can still pass in some strings and run them.

`eval("exec")` still gives us a message saying that `exec` is disallowed, but nothing about `eval` being banned. Apparently whatever is restricting us is
reading our input as a string and blocking keywords from a banned list. We can sneak past it, however: the restriction function isn't clever enough
to understand what `e = eval("ex" + "ec")` means, since it's doing a simple string comparison. We've now renamed `exec` to `e`, 
which the sandbox has no problem with.

With `exec` in hand, we can rewrite our original code and escape the sandbox.

```python
e = eval("ex" + "ec")
e("imp" + "ort os")
e("o" + "s.sys" + "tem('./i_escaped')")
```

I believe this is the intended solution. It's not the one I came up with first, however:

# Destroying the sandbox

When I first solved the problem, I only knew about `eval` and not `exec`, so I couldn't assemble the full solution. So let's suppose the sandbox writer
found out about this problem and patched it to ban `eval` as well. What could we do then?

Earlier I made the assumption that there was some kind of banned words list that was being used to block Python commands that would be useful to escape.
We can call `globals()` to see if something like that is in scope:

```python
{'whitelist': [], '__builtins__': <module 'builtins' (built-in)>, '__name__': '__main__', '__do
c__': None, '__file__': '/bin/shell', 'sys': <module 'sys' (built-in)>, 'e': <built-in function
 exec>, '__package__': None, 'code': <module 'code' from '/usr/lib/python3.5/code.py'>, 'restri
cted_terms': ['import', 'pty', 'open', 'exec', 'compile', 'os.system', 'subprocess.', 'reload',
 '__builtins__', '__class__', '__mro__'], 'banner': [...]}
 ```

 `restricted_terms` is a suspicious sounding name, and it has several terms we were banned from using. What if we just got emptied it out?

 ```python
 restricted_terms = []
 import os
 os.system("./i_escaped")
 ```

We're free to do anything we want at this point. At this point I watched the video to learn about `exec`, `compile`, and other useful things I could
have used to accomplish an escape- but attacking the implementation itself was satisfying in a completely different way.

I learned a lot from Kringlecon this year and I plan to do more writeups on some of the flags involved. Next time we'll take a look at
command injection with bash.