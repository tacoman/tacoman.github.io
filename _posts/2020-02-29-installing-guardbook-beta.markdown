---
layout: post
title:  "Getting the Guardbook beta"
date:   2020-02-29 21:00:00 -0500
categories: 
---

It's hard to believe, but we've been working on Guardbook for about a year now already. Access to public betas have been "just around the corner"
for about half of that time, but constantly pushed back in favor of fixing just _one more thing_ or adding _one more quick feature_ before we
got around to writing guides, handling access, and so on. Now the 2020 season is on us, and we have all of the core features we really need.
We need a strong beta program with dedicated testers to be able to keep working without the dev team losing their sanity on oversights.

# What you're in for

Even if it functioned correctly 100% of the time, the Guardbook beta would not be a substitute for your existing Guardbook. It uses an entirely
different database to allow us to test new features, which means that it's behind on real information. We will make an effort to periodically
sync the real data into beta, but the goal of the beta isn't to verify the content- only the code.

As you may know from my Twitter, push notifications are one of the biggest stress points for development- and while we think we've fixed
the bugs, there are new features coming which will include more changes to push in the year ahead. You may periodically receive a cluster of notifications
as we test these out- please let us know that you received them. (We'll also send a push to beta when we have new features that we want you to try out.)

The goal with the beta program is to give new features a week of testing with zero unresolved bugs before we push the same version to the rest of NGS.
We want people to be able to take their time with trying to push the program to its limits rather than feeling like they need to do a quick rush job.

Assuming that you're up for that, let's cover how to get into the program:

# Android

You have two options. The quick and easy method is to download the Expo app, which will allow you to beta test 95% of new features. Advanced users may choose
to sideload our beta APK, which allows testing the remaining 5%.

## The Expo method

Download the Expo app from the Play store. Once open, there should be a Projects tab accessible from the lower-left part of the screen. Choose "Scan QR Code".
Use a second device to visit [this link](https://expo.io/@ngsdetroit/app?release-channel=beta), and scan the QR code from the Expo app. Guardbook beta should
download automatically. To access it in the future, you should be able to access the new entry from the Projects tab without scanning the QR code again.

## The sideloading method

Download the beta APK [here](https://drive.google.com/open?id=1TCqRKCB2mBJH5PjKrnjXvWmfNp_4P0tq). On first launch it will likely load an old version- give it
a minute, force close the app, then re-open it and you should have the latest version.

If you choose this method, we assume that you can figure out the sideloading process securely on your own. If you are not comfortable doing so, use the Expo
method instead.

# iOS

There's nothing as quick and simple as the Expo method here, because Apple hates anyone trying to run a software team on our budget and level of organization.
You can request TestFlight access (the normal person's way) or sideload the IPA file (if you don't know what that means, do TestFlight).

## TestFlight

TestFlight is Apple's official way to let people beta test programs. We have to manually add you as a user to TestFlight first; shoot me a message if you'd like
to be added. Once you've downloaded a beta, it should be good for 90 days, during which it has the ability to update to further betas. After 90 days,
you will need to download a new beta build (and we'll have to upload a new one).

The upshot of all of this is that it's less complicated than sideloading on Android, but should still allow testing 100% of features as if you had sideloaded.

## Sideloading

Well, look at you doing things the hard way for fun! The IPA is [here](https://drive.google.com/open?id=1d3xhYfrB5AEWBQ4Gs_eb6hZrzafrrjWb). I'm not an iOS
user and I frankly don't know what would drive you to do it this way, but we provide the option.

# So what's next?

As of this writing (2020-04-29), we're slowing down development after a very intense offseason for the team. Getting set up in advance now is good and will make
sure you know when we do start testing new features, but it may be a bit before you have shiny new things to play with. But a sneak preview of what's to come:

## News feed: scheduled posts, channel subscriptions

We want to provide the communications team a way to schedule a post in advance (such as a merch drop) rather than be tied to their phones to hit the button
at the exact time. This means more tests that require push notifications, for example, as well as doing things like scheduling a news feed post and then
immediately crashing the server to see if it still delivers later.

For the users, we'll eventually start dividing up our news feed into different channels. Never interested in merch, but want to know every player announcement?
Love joke posts but you couldn't possibly travel to an away day? Channel subscriptions will be the answer one day, as well as a UI for selecting the exact channel
you want. Right now we have to walk the line between annoying some people with too many pushes while still providing the hardcore base with all the info a supporter
could want. Once we have news feed channels, we can set a few basic defaults and let the user control how much of a firehose they want.

## rtl language support and testing of localizations

If your phone is set to Spanish or German, Guardbook will recognize this and attempt to translate the entire UI. Thanks to work from @manuel_mg,
we even have Spanish translations for the player bios that are announced so far. We intend to add Arabic to this soon. Obviously we can't translate all content,
but we are committed to making the app as inclusive as possible as we move forward. Setting your phone to one of these other languages and looking for English text
in the UI is a great way to find bugs. (And yes, we specifically mean the UI- songs are not translated and there are not currently any plans for that.)

Arabic provides a unique challenge to us. Things that are aligned to the left should be aligned to the right instead when using a right-to-left language like Arabic.
We have a set of known bugs with this [here](https://github.com/Chattahooligans/hooligan-hymnal-app/issues/3#issuecomment-549560252), but we've continued development
since then and there may be more. Right now if you set your phone to Arabic, Guardbook will still load in English- but it will attempt to use the Arabic layout, which
will give you an idea of how things should look on screens like the roster. The content will still be usable with the mismatched alignment, 
but we'd like to polish everything as much as possible here.

## Lots of under the hood changes

Every so often we may ask you to just check that everything still works. We've taken on some technical debt to get this far in the time we've had, and it's time to pay it off.
If we do our jobs right, you won't be able to tell that anything changed- but it will be easier and faster for us to build more features and bring on more developers.
If we do our jobs wrong, it will quickly become very noticeable as things just stop working.

All of us at the Guardbook and Hooligan Hymnal team would like to thank you for joining the beta. There's been a great support structure in place to help us deliver
the best app that supporter culture has ever seen, and with your help we can make it even better.