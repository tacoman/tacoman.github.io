---
layout: post
title:  "Mastodon for the Apathetic"
date:   2022-11-11 18:00:00 -0500
categories: [Mastodon]
---

Twitter is on fire!
After years of saying that the birdsite is a bad influence on humanity, we might finally lose it forever!
Needless to say I'm excited.
I'd already started to move to Mastodon ahead of the buyout not because of Elon, but because I just think Mastodon is a better model.

If you're reading this you're probably less excited for Twitter burning than I am.
Somebody told you that Mastodon is the new Twitter replacement and now you feel obligated to check it out.
They're selling you this vision of a strictly better 1:1 replacement, but to you, it looks like a confusing mess.
The similarities to Twitter only make the differences more confusing.
Why can't it be simple and just let us post stupid GIFs again without Elon getting in the way?

I have _just_ enough hubris to think that I can convince you this isn't more confusing than technology you already use every day.
The technical aspects of Mastodon aren't too bad, and the culture is better.
You just need time to get used to both.

# Instances / Servers

This is the first roadblock everyone has to grapple with.
What do you mean I have to choose a server?
Why can't I just sign up for Mastodon and start posting?

The best analogy for this is email.
You didn't just "sign up for email", you got an account at someplace like Gmail, Hotmail, AOL, Yahoo, or Protonmail.
Those sites weren't all the same- Gmail was better at spam filtering, Protonmail had better privacy protections, etc.
But at the end of the day, you still had an email account and you could send messages to pretty much anyone else with an email account.

That's all the Mastodon server is. 
It's where your account lives, but so long as you don't pick an instance named something like `nazis.online` which everyone else has kicked off the network, you can talk to all of your friends on other servers too.
I'm on `freeradical.zone`, but I can talk to friends at `infosec.exchange` or `eldritch.cafe` or even `mastodon.social` without even noticing they're elsewhere.
All of our servers are automatically sharing our posts with each other.

So now you're still left choosing a server. 
You can use https://instances.social/ to set some rules for what you care about and search for a server based around your interests.
If you know a friend who's already there, asking them where they're at and how they like it is a great way to choose a server.
Generally the small and medium servers do a great job of actively moderating and kicking out entire servers full of nazis, so if you can find one of those, do it!
And if your server admin will accept donations, send them a few bucks- this is all being run by volunteers out of their own pockets, all because they believe in having a better web.

If you just want me to give you an answer, try signing up at https://mas.to. 
It's a general purpose instance, but it's not the default.
A lot of people will go to the "flagship" instance of `mastodon.social` instead, but I would suggest staying away from it.
A large part of what we want to build in Mastodon is a decentralized space where no one server can burn down the entire network the way Elon did.
`mastodon.social` is overloaded with new users and its admins _do_ see what they're building as a new Twitter.

# Timelines

Now you're signed up and you have several timelines.
Home?
Local?
Federated?
What on earth are all of these?

## Home Timeline

This is everyone you've followed and any posts they've boosted (think retweets). 
There is no algorithm trying to find things that make you angry and there are no ads.
It's just the posts in chronological order, as it should be.

## Local Timeline

This is everybody on the instance you signed up for, and it's one of the reasons why signing up for a server that's like your interests can be cool!
My server has a mix of leftist politics and information security-type folks, so checking out Local can be a good way to find likeminded people to follow.
If you were on a sports instance during a championship, going to Local would be a way to see everyone's posts during that without even needing hashtags.

## Federated Timeline

If you're reading this blog post, you're probably not interested in the federated timeline.
Just ignore it.
I do!

# Direct Messages

DMs work very strangely on Mastodon and I would mostly recommend using them to figure out how to contact somebody on another platform like Signal or Discord instead of carrying on long discussions in them.
It's not that they don't work, but there's a few pitfalls to be aware of, some of which are more serious than others.
To send a DM, you actually just write a standard post, then change the post privacy to "only the people mentioned".
That's considered a DM.

Fun fact- since the privacy setting is everyone that you @, if you somebody in the DM to talk about them behind their back, they'll appear in the conversation and receive the DM.
So don't go tagging people who aren't in the discussion.
Really, you should probably just be less of a gossip in general, but this post probably won't change your mind on that either way.

A lot of people on Twitter get alarmist about how your instance admin can read all of your DMs, and how they aren't end-to-end encrypted, and so on.
This is all true, but it was also true on Twitter, which doesn't do end-to-end encryption either- but we never heard stories of Twitter employees reading all your DMs.
I hate to break it to you, but you're probably not that interesting.
Your instance admin has an entire Internet in front of them, and your DMs are nowhere near the top of the list of interesting things going on.
It's one reason why you don't want to choose an instance run by a slimeball, but that's true of all technology.

# The Search is Broken?

No, not exactly, but it does work differently on purpose.
In almost every instance, you can't search the full text of a post.
You can search for hashtags and find them locally and on any posts that have reached your server, but you can't just search "DCFC" and find everyone who tweeted DCFC without the hashtag.

The good news is that this means you don't have to worry about random strangers showing up in your mentions because you said a "magic word".
If I make fun of Bitcoin, then Bitcoin fans and bots _cannot_ find my posts unless I actually tag it #bitcoin.
The days of censoring words in your posts to avoid bots are gone.
In fact, it's considered rude to censor words that way, because if somebody has filtered out "bitcoin", then me typing "b*tcoin" would bypass their filter.
If you're somebody who liked to search for random words to go cause trouble then you'll hate this, but it's another instance of how Mastodon isn't a Twitter replacement because it's against the worst excesses of Twitter.

Speaking of that:

# Culture

You should be able to get to following people and using Mastodon by now.
You're going to have an uncanny valley feeling for at least a few days as everything feels subtly wrong compared to how it was on Twitter.
That's expected- just keep using it and eventually you'll acclimate to the new interface and the way things work.
Most of the things you'll have to adapt to are cultural:

## No Quote-Tweets

It's a feature that was mostly used for finding things to negatively dunk on.
We don't do that here.
Mastodon isn't designed to suck you into a trap of rage bait for clout.
If you see something you don't like, just mute or block that person and get back on with your life.

## Content Warnings (CW)

People are relentless about the content warnings here.
Politics get content warnings.
Discussing your mental health?
Probably a content warning.
Workplace gripes?
I've seen those get CWs so people can just scroll past and get on their day.

What needs a CW and what doesn't is up to individual judgment.
If you're tired of having to click on them, you can get them automatically expanded by going to Preferences -> Appearance -> Always expand posts marked with content warnings.
They're there for your convenience, but if you can handle anything at any time, then you have that option.

However, refusing to put CWs on any of your own posts does make you a bad citizen here.
Yes, if I early voted and I've done everything I can for the election, I don't want to read your 45 posts about every little detail of the campaigns after that.
If you're posting about some fucked up act of violence, I want the option to see the CW and move past without having to see it and let it mess with my anxiety for the rest of the day.
On Twitter I'd just have to mute you, forget about that fact for six months, and then unmute you later when I remembered.
Here, you put a CW on.

## Image Alt-Text

Did you know that Twitter had a feature to put alt text on images, which none of us ever used?
Mastodon has the same feature- but you are expected to try to use it.
Nobody is going to get mad if you don't, but they'll likely prompt you to remember for next time, and you should make the effort.
There are plenty of blind people on the fediverse relying on screen readers, and the culture is that we do what we can to include them.

## Moderation and #fediblock

Your instance moderator(s) can and will kick people out just for being chuds.
Learn who they are- they'll respond a lot faster than Twitter Support ever did.
Somebody's a bad actor on another instance?
Whoever runs that instance can ban them.

If an instance seems to be built for bad actors or the mods there just don't do anything about it, you can mute the entire server all at once.
If you do, consider posting about it using the #fediblock tag.
This will help alert community moderators across the entire network about what's going on, and then can ban the entire server from talking to their own servers.
I have yet to interact with a single bad actor on Mastodon- literally not even once.
That's because our communities are proactive and really do stop people before they can get started.

## Go sign up!

You can follow me at @tacoman_x86@freeradical.zone.
Twitter gave me brainworms, but Mastodon just feels like hanging out with my fellow dorks again.
Let's keep the fediverse weird and kick out the corps when they try to influence it their way!