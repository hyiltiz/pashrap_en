---
layout: post
title: Watching Progress of Processes like dd via Signals
categories:
 - Software
tags:
 - Progress
 - Process
 - dd
 - ps
 - proc
 - Yanni
---
May 7 of 2013 is one of the best moments of my life. Yanni arrived in
Beijing, and we were able to be there at his convert. What a wonderful
night!

And one of my friend took his camera that night to capture the amazing
moments. And I must admit I was too noisy for him to catch a less
disturbing music concert. Anyway, it recorded my passion and Yanni's
delicate and sublime and beautiful musics.

Data Broken!
============

But nothing can be too perfect! (Is this because in perfectness there is
already a *too*?) 30 minutes of data cannot be played or even get copied
via `cp` or `dd` due to a I/O error, though the camera itself can play
all the files normally.

I used `badblocks` to find all the bad blocks in the card, and carefully
used `dd` to avoid reading those blocks of data, using `/dev/zero` to
fill them in. After this, a simple `cat a b c > full` and
`mount -o loop full /mnt` will help open all the files. Mission
accomplished!

The SD card was 32G, and using `cp` or `dd` gives no literally no
output, letting us unable to know how long we are gonna wait. Most of my
times I use `gcp` for this kind of big files, and since for this I had
to use `dd`, I looked up the internet for showing progress in `dd`. And
I found [a way to do it][].

Basically run the `dd`, and then send a `USR1 SIGNAL` to its process.

To illustrate, you run the following (valid, but perhaps not very
useful) `dd` copy:

        # It will run for a few minutes as it copies (and immediately discards)
        # 100 blocks of randomly generated data, each of size 1 KB. 
        $ dd if=/dev/random of=/dev/null bs=1K count=100 

        # To get a progress report while dd is running, you need to open
        # another virtual terminal, and then send a special USR1 signal to the dd
        # process.
        $ pgrep -l '^dd$'
        8789 dd
        # To send the USR1 signal to the dd prcoess:
        $ kill -USR1  8789

        # After reporting the status, dd will resume copying. You can repeat the above
        # kill command any time you want to see the interim statistics. Alternatively,
        # you can use the watch command to execute kill at a set interval.
        $ watch -n 10 kill -USR1 8789

I found out another similar way to watch the progress of the process
using the virtual filesystem `/proc/`. For the porpose described above,
simply run:

        $ cat /proc/8789/io

The output is not exactly the same with what you'd have using
`USR1 SIGNAL`, but it is much better than having nothing to look at when
you are having a cup of coffee.

[a way to do it]: http://linuxcommando.blogspot.com/2008/06/show-progress-during-dd-copy.html
