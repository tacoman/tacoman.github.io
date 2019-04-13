---
layout: post
title:  "Dynamic Taint Analysis: Further Reading"
date:   2018-4-12 17:00:00 -0500
categories: 
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/ERJnLYn7M5I" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Last night I delivered my first InfoSec talk to MiSec's Southfield chapter on Dynamic Taint Analysis. It was a great experience:
the prep work forced me to really do my research and learn more about the subject than I would have otherwise, and having my first
talk experience out of the way helped put that behind me and build up some confidence towards the next one. (Thankfully I had some long
dormant stage training to fall back on when it came to getting in front of a crowd of my peers!)

Unfortunately there's only so much information that you can cram into an hour long presentation- and I overcompensated for MiSec's
usual boisterous behavior by leaving room for more questions than I got. I wanted to make sure I had a deep enough understanding that I could
anticipate where people might ask further questions, so I read several white papers to supplement my knowledge. This blog post isn't meant to
explain what DTA is; for that, you can watch the talk. Instead, I'll talk a bit about my sources and elaborate on a few threads that were cut
short in the talk itself.

# _Practical Binary Analysis_ by Dennis Andriesse

[Practical Binary Analysis](https://nostarch.com/binaryanalysis) is one of the most interesting books I've read over the past year. It starts
by talking about the file formats of ELF and PE binaries and shows you how to read information from them via tooling or via hex editor.
It then takes a turn into a crackme-style chain of CTFs that use nothing but Unix tools, explains the principles of disassemblers, and then
gets heavy with chapters on Dynamic Taint Analysis and Symbolic Execution. This is how I learned about DTA in the first place. The exercises
are challenging without being unfair, and include everything from basic usages of the tools to writing custom disassembly to fool a disassembler
into giving incorrect output for what your program does. I highly recommend checking it out. If you want to try before you buy, the No Starch Press
link includes a link to the author's website where you can download a VM that's been pre-configured to run many of the tools described in the book,
as well as the code samples described within.

# The libdft whitepapers

[The original whitepaper](https://www.cs.columbia.edu/~vpk/research/libdft/) from the libdft authors describes their implementation strategy in greater
detail. I undersold the overhead in my talk; I described it as 30-100%, while the authors describe it as 14-600% depending on the use case. Something
to throw into my slide notes if I ever present this at another venue. The overall point that I was trying to make, that this is a huge performance
win over CPU emulation, still stands.

The authors also wrote another paper on [A General Approach for Efficiently Accelerating Software-based Dynamic Data Flow Tracking on Commodity Hardware](http://nsl.cs.columbia.edu/papers/2012/tfa.ndss12.pdf), which I have not read in as much detail. This describes the work that went into making libdft
fast in much greater detail.

# Advanced Evasion

[Anti-Taint-Analysis: Practical Evasion Techniques Against Information Flow Based Malware Defense](https://pdfs.semanticscholar.org/686a/cf7b87f2a0297fc2e0fd86755c0ebc3f7c17.pdf) goes into much greater depth on evasion techniques
than I had the time to. A particular favorite of mine is the discussion of how a multi-threaded program can introduce a race condition into
the taint propagation code without even trying to; a byte that should be marked tainted might have its tag cleared by another thread, or
the inverse could occur. The paper also describes some anti-evasion techniques, and includes a discussion of attacks from an untrusted program
extension (whereas my talk mostly focused on complete programs).

# It came from the GPU

One of the coolest ideas I had while doing research for this talk was to completely evade libdft by executing on the GPU instead.
This got reduced to a single bullet point in the talk. While checking for POCs for a GPU-based malware, I found
[You Can Type, but You Can’t Hide: A Stealthy GPU-based Keylogger](http://www.cs.columbia.edu/~mikepo/papers/gpukeylogger.eurosec13.pdf), 
Most reverse engineering tools in general are aimed towards the CPU, so this technique would require extra effort to solve all around.

I briefly touched on one mitigation technique for this: track all data flowing into OpenCL or CUDA via a taint sink, and if any tainted bytes come in, mark the entire output as tainted via a taint source. I also touched on how this could lead to false positives and overtainting if only a little of the input was tainted
and the entire output got marked as a result. OpenCL can also be forced to run on a CPU instead; modern versions of CUDA cannot. If you can force CPU
execution, that _should_ (I have not tested this) restore DTA to full functionality. For modern CUDA, I'm not aware of any implementations to get
around this currently. Theoretically, GPU emulation or recompiling the shader code might allow us to get around this; practically speaking, you'll
probably need to perform manual reverse engineering work on any GPU code for now.

# Legal and Technical Issues

libdft is distributed under the BSD license. Pintools are required to be compliant with the LGPL. Essentially, if you distribute your Pintool then
anyone who receives a copy must be able to get the source code for it, and they must be able to replace it within the system they are using. If you
deploy a product that has the Pintool baked in, you could potentially be required to open source your entire product under the LGPL. If you decouple them,
the Pintool will still be under the LGPL.

In my talk I described hooking into specific function calls and defining those as taint sources and sinks. The most common way of doing this would be to
leave symbols in your binary to allow you to find the address of the function involved. Most systems deployed externally strip these symbols for efficiency
and to leave less information for reverse engineers; leaving them in your binary might not be an attractive option. Distributing the source of a Pintool
that tells anyone who reads it what functions you consider interesting might be an even less attractive option. This is all on top of the execution overhead.

None of these are issues if you are developing and testing your tools completely internally, which is the use case I focused on in my Heartbleed example.
Research and lab work can be done without issue.

# Conclusion

DTA is an active field of research right now. My talk used libdft as a concrete implementation to discuss from an x86 perspective, but there are plenty
of other tools available for different platforms. It took me awhile to get an understanding of the concepts, and falling down the rabbit hole of learning
more provided days of entertaining reading and ideas. I'm looking forward to one day being able to move beyond exercises and apply these tools to
real world workloads.