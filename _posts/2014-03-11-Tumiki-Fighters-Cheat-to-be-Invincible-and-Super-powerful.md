---
layout: post
title: Tumiki Fighters Cheat to be Invincible and Super-powerful
categories:
 - Software
tags:
 - cheat
 - Linux games
 - code reading
---


Introduction
============

Among all those interesting games under GNU/Linux, [Tumiki Fighters](http://www.asahi-net.or.jp/~cs8k-cyu/windows/tf_e.html) is one of my favourite.

In this funny game, you can not only shoot and destroy your enemies, you can even catch their broken pieces for protection as well as for bonus points. They even shoot for you! Yes, the more you got those stuck pieces, the more it gets complicated to protect them. But don't worry! You can pull them in, so that you are small enough to dodge bullets! This time your bullet goes straighter than normal.


Mischief
========

There are many tricks and cheats that benefits (benefits?) the player. Espacially when it comes to POSIX compliant systems, such as GNU/Linux, Android, iOS, Mac OS X, BSD etc. You can look into the data files of the game, and also monitor the game process, and interfere its state.

For the latter, you can peek into `/tmp` while pausing the game, and saving the correspondsing data files if your game progress is promising. You can even change some data in `/tmp` and `/proc` in those corresponding areas. As this just may depend on how the software is implemented. You can play around if you are interesed.

We are going to enjoy the freedom that GPL gives us; run it as we wish, and modify if we'd like to. Tumiki Fighters is such a fun to play, and even more interesting if you prefer to poke around its source code. The game has been written by Kenta Cho <cs8k-cyu@asahi-net.or.jp>

Tutorial
========

Enough talking for now. Let's just go get its source, change whatever we like, and then compile it to have fun.

I am using Debian, following its `testing` branch. If you are using other OS, the basic procedure would be the same, but you may have to use your own package management system, such as `yum`, or `ports`.

First, get its source, and install the dependencies for successful compilation.

  $ sudo apt-get update & sudo apt-get upgrade
  $ sudo apt-get build-dep tumiki-fighters
  $ sudo apt-get source tumiki-fighters


So now we have the source code. What now? We can be super powerful, so that any enemy is nothing but another crunch standing in the way. Or, we can change the life system, so that we have more lives than the default 3.


Super Tumiki
------------

As for being super powerful, or shall we say, invincible, we can just change some of the data files that the games loads before running. It is not hard coded in order to be compiled. The file in this case, is about our own ship. We look at our game directory `/usr/share/games/tumiki-fighters/`. With commands like `find .` or `tree .`, the games directory structure is so obvious. In the last, you can find a file `./tumiki/myship`, where there is a table of numbers.

The file defines the pieces and their colors, the bullets, its attributes and speed, and how the pieces is combined. Backup the file with `cp myship myship.bak`, then change one parameter at a time, then run the game `tumiki-fighters` to see what is changed.

You can change the speed of your bullet, when it goes big enough, almost no enemy stands in your way. You can also make yoursolf very big, which helps you to stick enemies. Since you will die only when the *center of the red center piece* got bullet, it does you no harm to get superbig.

When you have enough found, remember to change the original file back, with `cp myship.bak myship`.


Invincible Tumiki
-----------------

So what about the lives? It would have been nice if we had five or more ships that the default three.

A exquisite analysis of the game directory `/usr/share/games/tumiki-fighters` does not help us with that. You find that those data is only relevant with the structure of the game play, such as how is your ship, how is enemy ship, and how is the boss, how does they fire and so on. But for your life, there is no clue. ( Please *DO NOT* go look for it yourself, because you are most likely to be not able to find anything relevant. I did that already. That was an interesting journey, yet quite time consuming.)

So we come up with the following hypothesis: the life you left is hard coded in the game source, and compiled into binary. If this is the case, we have to read the code itself.

We already downloaded the code, and you can find that the game is written in D, another programming language quite like C itself. If you are reading this, as you are now, you know basic English, and that is enough for reading and understating the source code. Do not freak away!

And we do not have to read all of the source, and understand how the whole program is written, just in order to change a default value of 3 to something like 20. Here we use `GNU coreutils` such as `grep`, `sed`, `awk`, and `find` to hunt down the beast.

        $ cd /the/path/to/the/source
        # recursively look for char 3 and write the output
        $ grep '3' -r . > out
        # 3 should be alone, unlike 32,a3,3f, which get filtered
        $ sed -i 's/^.*\w3.*$\n//g' ./out 
        $ sed -i 's/^.*3\w.*$\n//g' ./out 

The original `out` file was more than one thousand lines. After filtering the obvious ones we are not looking for, we have a file about two hundred lines. Far better, yet not good enough. The file is a list of lines describing the filename of the occurrences 3 in all the source directory, and the line in that file. You can read each line, and go on filtering using your intelligence. So far, AI.

I believe you are not patient enough to go over this list of 200 more lines. Good! I made sure that all the occurrences of 3 have *nothing to do with* the beast we are hunting!

Consider the scenario. What if the programmer implemented the left life such a way, that it is not 3? Say, what if it is a 2 we are looking for. In which case, the game is over when our life is less than 0, rather than equal to zero. Quite possibly what a programmer prefers. 

Rather than `grep`ping all the lines that has a 2 in it and then filtering through them, let's think of something else. We can look for keywords such as _game over_, _game control_, _life manager_ so on.

Or just read the documentation. The game is poorly documented. Yet you can still find something useful in the `README` file.

  > The ship extends at 200,000 and every 500,000 points.

Looking for a number like 200000 or 500000 is far easier than looking for 0,2,3! We found our beast! This has something to do with life control.

        $ grep '200000' -r .

All the occurrences is in the file `./src/abagames/tf/gamemanager.d`.
Now open the file, and change what needs to be changed.

        $ sudo gedit ./src/abagames/tf/gamemanager.d




        int score;
        const int LEFT_BONUS_NORMAL = 10000;
        const int LEFT_BONUS_EXTRA = 30000;
        int leftBonus;
        const int LEFT_NUM = 2;
        int left;
        const int FIRST_EXTEND_NORMAL = 100000;
        const int EVERY_EXTEND_NORMAL = 300000;
        const int FIRST_EXTEND_EXTRA = 200000;
        const int EVERY_EXTEND_EXTRA = 500000;
        int firstExtend, everyExtend;
        int extendScore;
        const int BOSSTIMER_FREEZED = 999999999;
        ####### some other code ######
        if (score > extendScore) {
          SoundManager.playSe(SoundManager.Se.EXTEND);
          left++;
          if (extendScore <= firstExtend)
            extendScore = everyExtend;
          else 
            extendScore += everyExtend;
        ####### some other code ######
 
The study got its significant result, at last! We see every once the `score` exceeds `extendScore`, your get another ship for bonus, see `left++` above.

So, change `LEFT_NUM` to some number larger that its original 2 (this is the proof that we should not have been looking for 3), to get your default life larger.

Change `EVERY_EXTEND_EXTRA` to about 200, so that about every 10 second in the game, you get another ship for bonus. Other numbers could also be changed to smaller, to get bonus ship quicklier.
 
Now we studied, and changed the code. Now build it, and run it!
 
        $ cd /to/the/source/path
        $ sh ./configure
        $ make

Now you can find the file `tumiki-fighters` in the source directory. Run it with `./tumiki-fighters`.

Have fun!
