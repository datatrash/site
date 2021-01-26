+++
title = "Shaving retro yaks during COVID"
date = 2021-01-26
+++
For the last few weeks I've been working on an assembler for the MOS 6502 CPU.
The name I chose for it is then, unsurprisingly, [MOS](https://mos.datatra.sh). Now, you may be wondering why I'm building this. After all, the world needs another 6502 assembler like it needs a hole in its ozone layer, right?

Well, no.

But this project isn't necessarily about practical read world use. Instead, it's probably closer to something like a [forever project](https://heredragonsabound.blogspot.com/2020/02/the-forever-project.html). It's not _supposed_ to be practical. It's also not something I originally intended to build.

When COVID hit, I initially wasn't that bothered by the fact that I'd working from home for a while. It's now nearly a year later and a certain gloominess has started to set in. To distract myself and keep my spirits up, I thought I'd have some fun by writing a game for the Commodore 64. This is the machine I grew up with and it's essentially the reason I became so interested in computers and programming specifically: I also wanted to be able to create something like those games I'd play every day.

When I was younger this was out of reach for me. I eventually learnt how to do some assembly programming and I even created a few intros for the cracking group Excess. Some of them have [survived](https://csdb.dk/scener/?id=6698) the ravages of time (thanks, [Sentinel](https://csdb.dk/scener/?id=903)!). That was still really simple stuff, though. Now, thirty years on, I convinced myself I'd amassed enough real world programming skills to take on that mythical beast: My own C64 game.

Tooling, of course, has improved massively since I was doing my C64 coding. For one, I don't need to do it on an actual C64 anymore. I found that a lot of people were using [Kick Assembler](http://theweb.dk/KickAssembler/Main.html) which is a nice cross-platform assembler written in Java. Together with a few Visual Studio Code plugins I cobbled together a relatively decent coding setup.

Just to warm up I first wrote a tile map scroller. This is a program that takes a [tile map](https://en.wikipedia.org/wiki/Tile-based_video_game) and allows the user to scroll across it using the joystick. This took me a fair bit of time since I had to relearn a lot of C64 coding techniques. Once I completed it I was happy with the results, and yet...

Although Kick Assembler supports some high-level scripting, it has enough quirks to make it a bit unwieldy to construct a full game out of individual subsystems. For instance, I wanted to make my tile map scrolling code completely configurable at compile-time. I also wanted to be able to add unit tests for it, because I've enjoyed having them for the last 15 years or so. These things weren't really possible.

So I looked at [KickC](https://gitlab.com/camelot/kickc), which is a compiler for a (variant of) C that targets the 6502 processor, the one used by the C64. It's certainly more high-level than raw assembler code, but it integrates nicely with Kick Assembler and even uses it for its inline assembler functionality. By the way, the names of the tools sounds similar and that's no coincidence, they're both created by programmers of the C64 demo group [Camelot](https://csdb.dk/group/?id=227).

I played around a bit with KickC but found out it didn't have a Visual Studio Code plugin to help me with things like syntax highlighting, error highlighting and the like. So, going one yak deeper in the Yak Stack, I tried configuring VSCode so that it would treat my KickC source files like a C subset. I quickly found that KickC doesn't actually return error messages in the GCC error format (e.g. `myfile.c:1:3: error: blahblah`). Going yet another yak deeper, I tried to [fix this](https://gitlab.com/camelot/kickc/-/merge_requests/1).

Around this time I was distracted by a newborn, so things lay dormant for a while. Once my paternity leave was over I decided I had found myself a new spare time project: My own 6502 tool suite. The Yak Stack was now so deep I might as well give in and try to build all of this stuff from scratch.

Over the last few weeks I've enjoyed myself tremendously during lunch breaks, spare 10 minutes between meetings, during the occasional quiet evening. Like all my spare time projects nowadays not involving Commodore 64s I'm writing my tool suite in Rust, and it's allowed me to explore a whole area of the Rust ecosystem I haven't really touched upon before. I'm parsing using [nom](https://github.com/Geal/nom), building a CLI using [clap](https://github.com/clap-rs/clap), automating my releases with [GitHub actions](https://docs.github.com/en/actions) and so on. I hope to spend some time learning about the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/) and [Visual Studio Code Extensions](https://code.visualstudio.com/api/extension-guides/overview) soon.

The most interesting part so far has been the thought process that goes into writing a toolable parser. By this I mean a parser that doesn't break on the first error, preserves whitespace and comments for source code formatting purposes and so on. I hope to write some more about these topics on this blog soon. I found [this blog post](https://www.eyalkalderon.com/nom-error-recovery/) especially enlightening.

Anyway, I'm not sure whether I'm actually going to release any part of this tool suite, but so far it's performing its original task: Lifting my COVID gloominess.