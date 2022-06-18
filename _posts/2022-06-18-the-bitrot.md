---
layout: post
title:  "The Bitrot: A Plea for Guardbook Developers"
date:   2022-06-18 12:00:00 -0500
categories: [DCFC]
---

First things first, let's make it publicly official: I've started the process of retiring from the organized aspects of the Northern Guard Supporters.
I didn't enter into this year intending to take that step; I thought I'd scale back from a few responsibilities and stick to covering the ones in my wheelhouse for years to come.
But I underestimated just how burned out I was- and then life circumstances came up that forced me to make a choice about how I could really do the most good with the limited time I have throughout the week. 
I've already stepped down from being a Discord admin. 
Everyone left in the moderators is somebody who I hand-picked and was given the nod by the universal consensus of the others in there.
The team has my full confidence and I rest easy knowing that everything is in good hands.

Guardbook, and by extension Hooligan Hymnal, however, are a different story.
Let me be clear up front: this is not a call-out post.
The Hymnal team is composed of great people who have accomplished a lot in these past few years.
We logged out of our day jobs and worked into the evening in order to provide something that's unique.
Something that's important, that gives a different model for how things could be done.
But the pace has slowed down until it's a near standstill.
We badly need fresh blood, people who are at a minimum interested in being caretakers of what was already built.
Ideally, the project could even move forward again- but we need maintenance work done in the meanwhile.

The good news is that the server and database are stable and should basically keep running for as long as our web hosts stay online.
It's the app portion- the part that you install on your phone- that has me worried.
We're now several months behind on the maintenance there- and aside from that killing forward momentum, that means that Guardbook might be a ticking time bomb.

# The Trouble With Expo

The Hooligan Hymnal platform uses [Expo](https://expo.dev/) as the app framework.
If you're unfamiliar, it basically uses React Native for the UI controls, and then adds in plenty of other platform integrations to allow you to write an app in 100% Javascript.
It has a cloud build service that will compile both Android and iOS versions of your app without you even needing to own a Mac.
(You still need a Mac to upload it to the app store, though.
A big thank you to Joseph Novak for always being there when I needed to upload.)
When you update your code, it'll automatically reload it into your simulator or your live device for debugging.
When it works, it's actually pretty slick.

The problem is that Expo upgrades their SDK incessently.
Think something like once every two months or so.
Generally they provide decent migration instructions, because they don't upgrade it in a backwards-compatible way; breakages are constantly occurring, and the code has to be updated to match.
But if you follow the directions, most of the time, you'll probably be fine.
I've done it a few times, but I was never the expert on the team at it.
UI frameworks just aren't what interests me about dev work; I tended to work more on the server and database side, only hacking on the frontend until somebody like Galen Riley would rescue it from my hamfisted attempts and make something beautiful for the rest of you.

This time, however, they've made a change that wasn't so easy to resolve.
If we upgrade the SDK to version 44, the Capo Dashboard / Gatekeeper Dashboard stops functioning.
There's a menu of buttons for them to tap on in order to create a post or make a few other changes- and the upgraded version doesn't seem to pass the taps through to the buttons.
This probably has something to do with some of the React Native libraries being old as well and finally hitting a mismatch- I've heard React Navigation thrown around with this.
I honestly don't know- this was always at the edge of my wheelhouse even when I had weeks where my day job had very little for me to do.
Now that my day job requires every ounce of technical energy I have during the day, I just don't have the mental capacity to figure it out. 
And for now it's not urgent, since the app is still functioning. Right?

# The Bitrot

So what happens if we just don't upgrade the Expo SDK?
Unfortunately, the negative impacts of that are already showing up.
Remember that fancy live reloading developer tool I mentioned earlier?
That requires being within the most recent versions of the SDK.
A new SG has tried to get on board with the Hymnal platform and ran into the test tooling not working for them some time ago.

Uploading a new build to the app stores?
Yeah, that also has SDK limitations.
Only some of that is Expo's problem- their build services also would like you to be on a reasonably up to date version.
But Google and Apple also periodically require their stores to have upgraded versions of _their_ SDKs- and getting to those requires updating Expo itself.
Software in the modern smartphone world, for better or for worse, cannot stand still- maintenance on the fundamentals just isn't optional.

You might wonder if we could just ignore updates entirely.
It's in the store and it works after all- can't we just leave it that way?
And the answer is that yes, we could just leave it that way- until we couldn't anymore.
On the first weekend that we launched, we ran into an issue where certain devices were crashing when they opened Guardbook- we had to cancel some promotions of it, and I had to go back, find the bug, and upload a new build.
There's nothing to say a new device couldn't come out that had a similar issue that suddenly caused crashes like that- look at store reviews of games long enough and you'll find one that doesn't work on any phone made within the last 2 years, yet is still up for sale.

But even beyond that, the stores add new rules every so often, and they perform spot checks on apps that already exist- and reserve the right to de-list them if you don't update to the new guidelines.
Most recently, I got an email from Apple saying that Guardbook looks like it might support creating an account, and if so, we have to let you delete the account from within the app.
Thankfully, we don't actually support account creation from within the app, so we should be OK- but this is just an example of how we can stand still and yet have the rules change from underneath us.

And with every SDK release that occurs without us keeping up to date, the problem is going to grow. 
Hopefully everything that's happening after SDK 44 will be a smooth and easy upgrade, but they might not be- and the task will only grow larger in time.
I know we have folks with the talent and drive to knock this out and keep the project healthy for years to come.
We need you to step up- to keep Guardbook from one day hitting a sudden issue that was years in the making.

Because if nobody does, the bitrot has already begun.