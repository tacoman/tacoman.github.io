---
layout: post
title:  "Detroit City Til I Die: The State of the Streams"
date:   2019-06-14 22:00:00 -0500
categories: 
---

*This is an archived version of a post at DCTID.com. [https://dctid.com/2019/06/the-state-of-the-streams/](Click here) for the up to date guide.*

Since I started supporting Detroit City FC, matchday streams have been one of the best examples of the club and supporters both working to provide a great experience. Home games have been broadcast by the team with a full crew, while supporters like Nick Miko would travel to away days and provide his own homebrewed feed at fields where our opponents weren't handling the job. This has even included some pretty entertaining [full commentary](https://www.youtube.com/watch?v=JUDBy1fvH_M). Some times a stream would break down and we'd be reduced to refreshing Twitter for updates- the dreaded "twatch party". ("Professional" organizations fell victim to this more often than a Miko feed. Just saying.)

2019 has been an interesting year for streaming. The NPSL has established an official streaming partner in MyCujoo. In theory it's a good move- the question of whether you should look on Facebook, Youtube, a club's website, or somewhere else entirely for a stream goes away, so long as that team is streaming at all. A consistent interface no matter who's home field you're on should be a step forward.

MyCujoo's player is inconsistent, however. Streams will drop resolution more frequently than on providers like YouTube. They're delivered in five second slices, which creates a series of noticeable frame skips on some computers. The network will hiccup at times- usually timed to introduce the most anxiety possible, like during an attack.

I got to learn about this after coming home from a weekend-long trip while trying to watch a home game. With a little work we can work around most of these issues- it can't guarantee a high-quality stream (you're still at the mercy of the uploading team to have a good setup), but it can at least remove some of the worst issues.

# Fixing the Streams

*One Time Only*:

* Install the browser extension Video DownloadHelper. [Chrome](https://chrome.google.com/webstore/detail/video-downloadhelper/lmjnegcaeklhafolokijcfjliaokphfk?hl=en-US) / [Firefox](https://addons.mozilla.org/en-US/firefox/addon/video-downloadhelper/)
* Install VLC

*Starting a Stream*:

* Find the stream. For a DCFC home game, this is usually at https://detcityfc.com/watch. Otherwise, you may need to do some hunting in MyCujoo.
* Start the stream inside your browser so Video DownloadHelper can find it.
* Click the Video DownloadHelper icon in the browser's toolbar. You should have several options available, one for each resolution: find the one with the highest resolution and click the arrow next to it. 
* Click "Copy URL"
* Open VLC
* Media menu -> Open Network Stream
* Paste your URL into the "please enter a network URL" text box
* Check "Show more options"
* Set the caching option to 15000ms
* Click play
* (Optional) if you have a Chromecast, Playback -> Renderer can find it and re-stream the video to there. (At the time of this writing, my copy of VLC is not finding my Chromecast, so I would need to directly connect my laptop to my TV's HDMI.)

This is a lot more steps than just clicking "play" as many of us are used to. There's some major benefits, though: VLC will force the stream to play at the highest quality available. It's faster on many older computers than attempting to load the stream in a browser. And finally, this will give you a 15 second buffer before it starts. If the stream has a hiccup, VLC will keep playing from the buffer and recover without you noticing in most cases. (If the stream goes down for longer than 15 seconds or your connection can't keep up, you'll still see hiccups, of course.)

We tested this for the Grand Rapids away match at the City Clubhouse and it worked perfectly. (Thanks for letting me test my mad theories on an official computer, Sean!) The framerate was low, but I think this was down to Grand Rapids' infrastructure and not MyCujoo or VLC.

*Final thoughts*

After a major Tweet storm, DCFC has scheduled a number of regular NPSL season home games for simultaneous streaming on YouTube. This would remove a lot of work. Unfortunately, so far we've only seen this tested for the FC Indiana match. MyCujoo started on time, but Youtube started about 21 minutes late. I'm confident this issue will be worked out soon, but in the meanwhile you might want to open both sites in separate tabs while waiting to see which one will launch on time.

Some clubs have followed suit. Grand Rapids streams on YouTube now as well. Ann Arbor is on MyCujoo. FC Indiana still relies on the power of Miko. If you can find a YouTube stream, I'd suggest you use that.

If you run into any issues with this guide or have any other suggestions on how we can make streaming easier this year, please find me on Twitter: @tacoman_x86. We'll keep this post updated as the situation changes or until it becomes unnecessary.
