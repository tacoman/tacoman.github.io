---
layout: post
title:  "Learning OSINT with the Trace Labs Global CTF"
date:   2019-02-02 20:40:00 -0500
categories: 
---

I first learned about the concept of footprinting through a used copy of _Hacking Exposed_ that I bought as a teenager.
The concept seems to be better known as OSINT today, or Open Source Intelligence, but either way its always been a fascinating part of InfoSec
for me- how much information can you get on a target using only publicly available information? It's frequently used in the context of
gathering information on a company in preparation for an attack, simulated or otherwise. A few well-crafted Google or social network searches
could expose plenty of information on your target's infrastructure, on IT personnel to impersonate, of employees to target directly for a
phishing attempt.

I've never done the corporate thing- I've learned about it, read about it, listened to podcasts on it, but I've never had a good reason to just
sit down and build a dossier. I'm sure it could be a fun exercise, but I'm not a professional penetratation tester, so making any further use
out of it would likely end with sitting in a jail cell and wondering about who's chatting up my wife while I wait. What I _have_ done is
doxxing certain friends who were preparing to follow through on suicide threats before the worst could happen. Finding addresses,
getting family members' phone numbers so I could alert them- it's one of those skills that can either save a life or ruin it depending on
who's wielding it.

So learning more OSINT techniques was on the "eventually" list- right after I burned myself out with all the other areas of InfoSec that
I'd reignited my interest in over the past year, probably. Then someone dropped the news that [Trace Labs](https://tracelabs.org) was running
an OSINT CTF in search of missing persons. With nothing else on the CTF schedule yet and with an amazingly good cause on the line,
I decided to set down the reverse engineering books and get prepared for a new kind of challenge.

# Restricted Engagement

The rules for the CTF imposed more limits than any of my past info hunting experience. Everything had to be truly _open_- you had to include a URL
for verification. There was zero tolerance for contacting any friends or family of the missing people and asking questions. This all makes
perfect sense- a flood of helpful hackers interrogating people is not only disturbing and going to increase the heartache of the families involved,
it could even spook any kidnappers into rash action if they get messaged. Also, law enforcement is already involved in all of these cases- Trace Labs
sends all data to law enforcement to help them with their hunt. No sense in repeating what the professionals have done in terms of interviews.

So if professionals are involved, what do they need us for? Not all law enforcement has the training or staffing to gather the kinds
of data that CTF players might have the knowledge to find. Combine that with the effects of many minds going in different directions and
the hope is that we'll be able to find those few extra clues that will help the police close the case out. From the perspective of the CTF
players, it provides a platform for training OSINT skills- and Trace Labs also steers people towards training materials while working on their own courses.
Playing with a team allows people to learn together, like any other CTF. So long as everyone's playing within the rules- and so far as I know,
there isn't a problem with people breaking them- then everyone benefits.

# RTFM

I knew I needed more structure in my learning if I was going to dive into this on the few weeks' notice we had. I picked up a copy of
Michael Bazzell's _[Open Source Intelligence Techniques: Resources for Searching and Analyzing Online Information](https://www.amazon.com/gp/product/1984201573/ref=dbs_a_def_rwt_bibl_vppi_i0)_ and scanned through it- not reading it deeply cover to cover, but giving myself a high-level overview so that
I knew what was possible and could return to it for specific techniques later. This preparation happened concurrently with several other side-projects;
I don't mean to spoil the ending of this post, but it showed.

That said, I still learned a lot from it. My initial temptation to simply reactivate old social media accounts or use my current ones was
quickly disabused when it was pointed out that this could leave traces such as my name coming up in Facebook or Twitter's "You may know this person"
feature. I'd need to create burner accounts and dispose of them at the end of the CTF, as well as discarding my VM. Fortunately Bazzell provides
a customized Linux VM named Buscador pre-loaded with OSINT tools. You might think of it as the Kali Linux of OSINT. I loaded up an instance
ahead of time and procrastinated on making the burners. How hard could it be to make a few quick accounts and run them the day of?

I'm not going to write a full review of the book, but it's very good. It combines basic tenets of tradecraft with a rich library of
resources to search for information and techniques to get the most out of them. Bazzell demonstrates how to write very particular searches
for different sites, has written automated pages on his websites to help do the dirty work, and gives a quick overview of tools
like [Recon-ng](https://bitbucket.org/LaNMaSteR53/recon-ng). If you're interested in the subject, I highly recommend it.

# Falling flat

After some initial confusion about logistics and who was available, we decided to run the game remotely over Slack. This didn't kill
all collaboration, but it did remove a certain sense of energy and added a little bit of friction at our experience level. A couple hours before the
game started I registered my burner social media profiles. Instagram accepted me readily and without question, thankfully. Twitter and
Facebook decided within an hour that I was "suspicious"- which appears to be their way of saying that I hadn't provided enough information.
But I could get them off my back by simply providing headshots, phone nummbers, and all the other kind of identifying information that I didn't
really want to assign to an account meant to evaporate at the end of the day. Twitter did this all on its own- Facebook displayed the message
when I tried to login later with Tor. Whether it would have flagged me regardless of this I'm not sure- and while I'd heard before that Tor
logins can trigger many sites, I simply hadn't thought of it when I opened Tor to test it out.

So the game started with our ability to retrieve information from social media being severely hampered. The format involved 8 missing people
being listed from various countries, with different point values assigned for pieces of information ranging from their home address all the way
up to clues about their current location. Data found on a law enforcement site was worth zero points since they already had the information.

Going into this I had a reasonable amount of confidence in myself. I've taken online friends who I'd never met in real life and hadn't even been
that close to begin with before and pinned down exactly where they lived before in short order- I'm good at this, right? No, in fact I'm
very bad at this. I was effectively inside the perimeter in those previous cases- already social media friends with full access, able to talk
to their contacts and mine, and so on. Trying to locate a complete stranger is another thing- and even when you do find their home address,
that's still a relatively low-valued flag. (If they were at home, they'd probably also not be missing.)

So I'm not going to go into deep detail about the individual flags like I did in previous CTF posts. Even if I'd laid out brilliant cases that found
these people, it would be insanely irresponsible to just publish it online the same day. What I can say is that we did successfully find social
media profiles through some quick digging. In a few cases we found home addresses. But trying to take those usernames and find other usages of them
came to little. Digging deeper into social media profiles was generally impossible with our burners locked out. And while I used many of Bazzell's
tools to keep digging, I struck out more than I succeeded. 

Some of this was inexperience with using the tools effectively; some of it might have been not enough persistence.
With many CTFs, you know there's an answer and you can come back and hit it harder after a few minutes. With this one, there's no guarantee
of finding any answers at all. The scoreboard made it very obvious that we were missing things, but our answer was frequently to move on
and see if there was any lower-hanging fruit on the next target rather than stick it out with the current one. But with six hours and eight
contestants, it was too easy for our team of only two people to decide that we needed to cut our losses and hope that the next one would
be more cooperative.

# Red Teaming your friends!

```
<jtrevner> if you get bored I have a suggestion
<tacoman> I'm listening
<jtrevner> Help me find my stuff so I can delete it
<jtrevner> You’ll have no problem find stuff on me
```

My partner for this CTF was [J.T. Revner](https://www.jtrevner.com/), who joined #misec shortly after I did. He's one of the most OPSEC
focused members of the group that actually shows up to meetings in person. For him to directly suggest this was a surprising indicator
of the level of trust he'd already chosen to place in me to not do anything malicious. J.T. was also investing in Bazzell's other book,
which was all about scrubbing signs of yourself and reducing your exposure to OPSEC efforts. So as frustration mounted with our inability
to find actual missing persons, I took on the challenge of finding information leaks on him instead.

He gave me a list of existing handles, emails, and even his real name(!), and I went to see what I could find. And honestly, I didn't have
to go as far as you might think to make him uncomfortable with what was out there. (And yes, he's got to vet this post and redact this
section before publication. Just because it's OSINT doesn't mean I'm going to freely republish against someone's will.)

* A dotfiles repo that leaked both his platform of choice and an employer
* A few political social media interactions from other users directed at an otherwise inactive account
* Reddit showed up, but the post in the preview was conspicuously missing. He confirmed that this had been due to a recently deleted
account, but the search engine hadn't caught up yet.
* LinkedIn provided a giveaway on his true identity.
* archive.org gave away some extra info on his past doings.

```
<jtrevner> Depending on how this goes I might have to kill this name IDK
<jtrevner> But for someone who claims to care about privacy, Im not doing a good job
```

For what it's worth, I think that's a little harsh of a self-assessment. It's hard to live as much of your life online as many members of #misec
do and not leave a trail. J.T. has a lot of knowledge to share and is trying to walk the line between having a public platform to do so
while also trying to be invisible to the worst parts of world. Scrubbing out a few pieces of info would go a long way towards improving this.
Perfection is impossible- some trails can't be scrubbed entirely. It's a valuable lesson in how even a well-guarded pseudonym can become
a liability over time.

# Endgame

A big thanks to Trace Labs for running this- preparation, completion, and manually vetting all incoming data impartially is a major task
and for an amazing cause. Learning more OSINT skills might have perpetually been on my "eventually" list without this event. I've come out
of this with a much deeper respect for those who are great at OSINT or who do it as part of their day jobs. Hopefully next time one of these
happens we can get more people involved and step up our game.

Be on the lookout for @jtrevner's follow-up to the last section of this post, tentatively titled "Blue Teaming your friends". He'll be providing
some examples of how to clean up your trails and remove them from OSINT hunters.