# Basic (Bespoke)BareBonesBash(BroughtByBlissfullyBaffledBioinformaticians)
A basic Bash tutorial by [James A. Fellows Yates (@jfy133)](https://github.com/jfy133) and [Thiseas C. Lamnidis (@TCLamnidis)](https://github.com/TCLamnidis).
<p align="center"><img title="Source: https://giphy.com/gifs/v58q1se3dZvag" src="https://media.giphy.com/media/v58q1se3dZvag/giphy.gif" width="40%"></p>

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><p align="center"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

## Table of contents
   * [(Bespoke)BareBonesBash(BroughtByBeardedBioinformaticians)](#bespokebarebonesbashbroughtbyblissfullybaffledbioinformaticians)
      * [Introduction](#introduction)
      * [tl;dr](#tldr)
      * [Navigating the maze](#navigating-the-maze)
      * [Playing with files, one bit at a time](#playing-with-files-one-bit-at-a-time)
      * [Asking the computer for help (it loves helping people)](#asking-the-computer-for-help-it-loves-helping-people)
      * [The Lord of the Pipes: One command to do them all.](#the-lord-of-the-pipes-one-command-to-do-them-all)
      * [Now you're thinking with portals! Symlinks and their usefulness.](#now-youre-thinking-with-portals-symlinks-and-their-usefulness)
      * [Lazyness 101: Minimising our work by maximising the work of the computer](#lazyness-101-minimising-our-work-by-maximising-the-work-of-the-computer)
         * [Text Editing in Terminal](#text-editing-in-terminal)
         * [What is a Variable anyway?](#what-is-a-variable-anyway)
         * [Loop de Loop](#loop-de-loop)
      * [The road so far](#the-road-so-far)
      * [<em>OPTIONAL:</em> The Cleanup Crew](#optional-the-cleanup-crew)
      * [For next time!](#for-next-time)

----
## Introduction

The aim of this tutorial is to make you familiar with using bash everyday... 
for the rest of your life :smiling_imp::trollface:. More specifically, we want 
to do this in the context of bioinformatics. We will start with how to navigate 
_\[Thiseas insisted on that fancy word...]_ around a filesystem in the 
terminal, download sequencing files, and then to manipulate these. Within 
these sections we will also show you simple tips and tricks to make your life 
generally easier. In fact, some of these commands we only just learnt last week 
_\[Thanks Aida!]_ and we've been using the terminal for more than 2 years.

This tutorial is designed to be self sufficient using public data. Thus you
can do this anywhere on any machine with a UNIX terminal (no warranty provided).

<p align="center"><img title="Source: https://tenor.com/view/starwars-confusion-jake-lloyd-anakin-skywalker-confused-gif-4813240" src="https://media1.tenor.com/images/2c42ed493c000f048a561e8217ef9611/tenor.gif" width="40%"> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <img title="Source: https://giphy.com/gifs/i-then-zZfNOVP35Nrkk" src="https://i.giphy.com/media/zZfNOVP35Nrkk/giphy.webp" width="40%"><br /><i>
You BEFORE this tutorial. &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; You AFTER this tutorial.</i>
</p>

## tl;dr

If you want to know what you will learn in this tutorial, or are already too scared 
to read the rest of this tutorial, you can look at this table as a quick reference. 
To understand actually what each command does, carry on reading below!

| command | description                        | example                                    | common flags or arguments    |
|---------|------------------------------------------------------|------------------------------------------------------------|--------------------------------|
| pwd     | print working directory                  | pwd                                      |                  |
| ls    | list contents of directory               | ls                                         | -l (long info)           |
| mkdir   | make directory                       | mkdir pen                                    |                  |
| cd    | change directory                     | cd ~/pen                                   | ~ (home dir), - (previous dir) |
| ssh   | log into a remote server                   | ssh <pen>@<apple>.com                        | -Y (allows graphical windows)  |
| mv    | move something to a new location (& rename if needed)| mv pen pineapple                           |                  |
| rmdir   | remove a directory                   | rmdir pineapple                          |                  |
| wget    | download something from an URL             | wget [www.pineapple.com/pen.txt](https://media.giphy.com/media/10fVn57KfQ8Wkw/giphy.gif) | -i (use input file) |
| cat   | print contents of a file to screen           | cat pen.txt                            |                  |
| gzip    | a tool for dealing with gzip files           | gzip pen.txt                             | -l (show info)           |
| zcat    | print contents of a gzipped file to screen       | zcat pen.txt.gz                            |                  |
| whatis  | get a short description of a program         | whatis zcat                              |                  |
| man   | print the man(ual) page of a command         | man zcat                               |                  |
| head    | print first X number of lines of a file to screen  | head -n 20 pineapple.txt                         | -n (number of lines to show)   |
| &#124;  | pipe, a way to pass output of one command to another | cat pineapple.txt &#124; head                    |                  |
| tail    | print last X number of lines of a file to screen   | tail -n 20 pineapple.txt                       | -n (number of lines to show)   |
| less    | print file to screen, but allow scrolling      | less pineapple.txt                           |                  |
| wc    | tool to count words, lines or bytes of a files     | wc -l pineapple.txt                          | -l (number of lines not words) |
| grep    | print to screen lines in a file matching a pattern   | grep pineapple.txt &#124; grep pen                 |                  |
| ln    | make a (sym)link between a file and a new location   | ln -s pineapple.txt pineapple_pen.txt            | -s (make _symbolic_ link)      |
| nano    | user-friendly terminal-based text editor       | nano pineapple_pen.txt                     |                  |
| rm      | more general 'remove' command, including files     | rm pineapple_pen.txt                     | -r (to remove directories)     |
| $VAR    | Dollar sign + text indicates the name of a variable  | $PPAP=Pen                          |                  |
| echo    | prints string to screen                | echo $PPAP                           |                  |
| for     | begins 'for' loop, requires 'in', 'do' and 'done'  | for p in apple pineapple; do <br /> echo "$p$PPAP"; done <br /> <i>applePen pineapplePen</i> |                  |


## What is a terminal?

A terminal is simply a fancy window that allows you to access the command-line interface
of a computer or server.

The command-line itself is how you can work on the computer with just text.

`bash` (**b**ourne **a**gain shell) is one of the most languages used in the terminal. 

<p align="center"><img title="Source: https://i.imgur.com/BkDkTxY.jpg" src="https://i.imgur.com/BkDkTxY.jpg" width=55% ></p>
_\[Combine the two and become L33T H4X0RZ\]_

## Navigating the maze

After opening the terminal what you will normally see is a blank screen with a
'command prompt'. This typically consists of your username, the device name, a 
colon, a directory path and ends with a dollar symbol. Like so:

```bash
<username>@<device_name>:~$
```


Throughout this tutorial, we will indicate the prompt of each command just with 
a single `$`, without the rest of the prompt. Make sure NOT to copy the `$` 
as the command won't work! This symbol is important for reasons you will see 
later.

Furthermore, the symbols`<>` are used to show things that will/should be 
replaced by another value. For example, in Thiseas' command prompt `<username>` 
will be replaced by `lamnidis`, as that is his username. 

Keep an eye out for both of these throughout the tutorial.

<p align="center"><img title="Source: https://giphy.com/gifs/studiosoriginals-gilphabet-3o84U72tKO389H2lI4" src="https://media.giphy.com/media/3o84U72tKO389H2lI4/giphy.gif" width="20%"></p>

Note that prompts _are_ customisable, so they will not always be displayed as 
above _\[look at Thiseas' magical prompt as an example. James keeps his vanilla as he is a barbarian]_.

The prompt is never involved in any command, it is just there to help you know
who and where you are. Therefore you must always make sure when copying a 
command (see later) that you do **NOT** include the prompt.

Here, the directory `~`, stands for your home directory. This shorthand can be 
seen and used both on your machine and on the cluster. Note that this shorthand 
will point to a different place, depending on the machine and the user.

If you want to know what the shorthand means, (here comes your first command!)
you can type in `pwd`, which stands for "**p**rint **w**orking **d**irectory". 
The working directory stands for whichever directory you are currently in. 

```bash
$ pwd
```

This prints the entire "filepath" of the directory i.e. the route from the "root" 
(a specific directory on the machine), through every subdirectory, leading to your 
particular folder. 

There are two types of filepaths: 
* An **absolute** path will start with the deepest directory in the machine, 
  shown as a `/`. Paths starting with `~` are also absolute paths, since `~` 
  translates to an absolute path of your specific home directory. That is the 
  directory path you see in the output of the `pwd` command you just ran.
* Alternatively a **relative** path always begins from your working directory (i.e.
  your current directory). Often this type of path will begin with one (`./`) 
  or two (`../`) dots followed by a forward slash, **but not always**. In the 
  syntax of relative pathways `.` means "the current directory" and `..` means 
  "the parent directory" (or the 'one above'). 

As a real life example, imagine you are walking down the street when a car 
stops to ask for the way to the Brandenburger Tor. You could tell them how to 
get to the Tor from Ethiopia (since that is the presumed root where all humans 
started their journey) _\[haha, human history joke]_, or you could say "Take 
a left here, straight for 3 blocks, and you're there.". The latter set of 
directions is relative to their current position, while the first one is not.

<p align="center"><img title="Source: https://giphy.com/gifs/teamcoco-germany-berlin-3o6Ztk4xTVAnfqYPn2" src="https://media.giphy.com/media/3o6Ztk4xTVAnfqYPn2/source.gif" width="20%"> <img title="Source: https://giphy.com/gifs/guys-call-ethiopia-QWXhaNjfwuNs4" src="https://media.giphy.com/media/QWXhaNjfwuNs4/giphy-tumblr.gif" width="20%"></p>

Now let's look around at our current location and see what we can find within 
our home directory. We can use the command `ls`, shorthand for "list", which 
will (surprise surprise) list the directory contents.

```bash
$ ls
```

Your home directory should come equipped with multiple subdirectories like 
"Documents", "Pictures", etc. 

It is now time to start moving _\[navigating]_ towards "the Brandenburger Tor" 
from the example above. We can navigate through directories using the command 
`cd` which stands for "**c**hange **d**irectory".

```bash
$ cd Documents/
```

This command will move you from your home directory to its "Documents" 
subdirectory. Note that `Documents/` above is indeed a relative path, since it 
starts from the home directory (the initial `./` is implied). To find the 
absolute path of the "Documents" directory we will once again use `pwd`.

**BONUS TIP TIME!** You can use the <kbd>&uarr;</kbd> and <kbd>&darr;</kbd> to search through your 
last 1000 used commands.

```bash
$ pwd

```

Now we can move up one directory, back to your home using the relative path
`../`.

```bash
$ cd ../

```

We can also change directories using absolute paths. Lets do this using the 
absolute path we printed using `pwd` in the previous step. Type `cd`, but don't 
press enter yet! 

<p align="center"><img title="Source: https://giphy.com/gifs/cant-23BST5FQOc8k8" src="https://media.giphy.com/media/23BST5FQOc8k8/source.gif" width="20%"></p>

Copy and paste the output of the previous `pwd` command 
(which you can see in your terminal does not have the command prompt), after 
the `cd`, then press enter. **NOTE:** Putty users have to highlight the text 
and it copies automatically, and use right click or `shift + Insert` to paste.

For example:

```bash
$ cd /home/fellows

```

**BONUS TIP TIME!** Now for one last move, here is a lesser-known trick. When 
using `cd` you can use a dash (`-`) to indicate 'my previous location'. This is 
useful since you can traverse _[ha! I have my own fancy words now! - James]_ 
multiple directories with one `cd` command. So, now, to return to our home 
directory from the documents directory we can type:

```bash
$ cd -
$ pwd

```

And voilá! We are back in our home directory. Now try running this:

```bash
## Remember in "A land before time" when the dinosaur's mother died?
```

While reading that command, you 
might have been reminded of one of the most emotionally devastating moments of 
any person's life. However, the computer would show no signs of emotional 
struggle. Sure, computers don't have feelings and all, but **ALSO** the 
computer never even read that sad reminder. A computer will **NOT** read 
anything that comes after a _comment character_, which in bash is a hash (`#`) 
_\[NOT a hashtag!]_. You can use comments to explain what a certain bit of code 
does, without affecting how that code runs. This can also be a useful lifehack 
in certain situations, an example of which will be given later.

<p align="center"><img title="Source: https://www.buzzfeed.com/bradesposito/sad-before-time?utm_term=.cjY4banJZ#.ixJ815NjJ" src="https://img.buzzfeed.com/buzzfeed-static/static/2015-04/29/21/enhanced/webdr15/anigif_enhanced-31175-1430357953-19.gif" width="35%"></p>

However, often when working in bioinformatics we will be working remotely on a 
server. The most typical way is to log in via "**s**ecure **sh**ell", known as 
`ssh`. Note that you can normally only log into an institute's server being on 
the network of the institute and or via VPN, so make sure you are on either of 
those.

If you're working just on your personal computer, skip to the [next section](#where-am-i)!

----

A typical `ssh` command consists of the `ssh`, with a user, '@' symbol and then 
the address of the server. For example:

```bash
$ ssh <user>@<server>
```

You can find our your user and server from your IT department.

----

Now, looking at your terminal you will see `~`. In bash `~` points to a 
different home directory, as you are on a different machine. However, all of 
the commands you've learned so far will still work the same :wink:. You can 
double check both of these by typing 

```bash
$ pwd

```

It is important to keep your corner of the servers well organised, and the 
trick to doing that is making your own directories. Often _a lot_ of them. 
You can make a new empty directory using the command `mkdir`, shorthand for 
"**m**a**k**e **dir**ectory".

```bash
$ mkdir ~/BareBonesBosh
$ ls ~

```

You can now see your new and devoid-of-content directory. But don't celebrate 
yet! The directory has the wrong name! _[Who could have seen _this_ coming?]_ 
If you saw the typo and fixed it already, NO BROWNIES FOR YOU! 

<p align="center"><img title="Source: https://giphy.com/gifs/table-flip-ieGdB2g5kDIkg" src="https://media.giphy.com/media/ieGdB2g5kDIkg/giphy.gif" width="20%"> <img title="Source: https://tenor.com/view/it-crowd-moss-computer-throw-gif-5404468" src="https://media.tenor.co/images/d82c7edc4b04227b4c973f24b904695f/raw" width="26%"></p>

But don't lose hope, as we can rename things with the `mv` command, 
shorthand for "**m**o**v**e". 

In fact move, as the name suggests, will move a file/folder into a new location, 
also renaming it in the process if necessary. It works by typing `mv`, the old 
location and a target location.

```bash
$ mv ~/BareBonesBosh ~/BearBonesBash

```

The command above will now move the directory into the same location, but
as the target location is spelt differently, the directory will now have a 
different name. Thus, essentially renaming it to `BearBonesBash`. 

But oh no! Not again! This is not a bash tutorial for ancient bear genomics! 

<p align="center"><img title="Source: https://giphy.com/gifs/bear-forest-water-IQ9KefLJHfJPq" src="https://media.giphy.com/media/IQ9KefLJHfJPq/giphy.gif" width="20%"></p>

Let's just delete that empty directory and start over, using the `rmdir` 
command, short for "**r**e**m**ove **dir**ectory".

```bash
$ rmdir ~/BearBonesBash
$ ls ~

```

And now we can create our directory, properly named this time.

```bash
$ mkdir ~/BareBonesBash

```

## Playing with files, one bit at a time

So we have places to organise our files... buuut we don't have any files yet! 
Lets change that.

We ain't playing with bears today - that's dangerous (as we saw above), instead,
lets play with some Mammoths!

<p align="center"><img title="Source: https://giphy.com/gifs/sid-ice-age-a-mammoth-christmas-kbuQOkATEo6VW" src="https://media.giphy.com/media/kbuQOkATEo6VW/giphy.gif" width="20%"> <img title="Source: https://giphy.com/gifs/3o6Zte5Q11lxAu8Q5q" src="https://media.giphy.com/media/3o6Zte5Q11lxAu8Q5q/giphy.gif" width="20%"></p>

We're going to use `wget` to download a FASTQ file from the ENA (European Nucleotide Archive). So while in 
our `~/BareBonesBash` directory, we will give `wget` the link to the file, and 
we should see a loading bar. Once downloaded (it should be pretty quick),
we can use `ls` to check the contents.

<p align="center"><img title="Source: https://giphy.com/gifs/mario-kart-lAIbbDbcXSZSU" src="https://media.giphy.com/media/lAIbbDbcXSZSU/giphy.gif" width="20%"></p>

```bash
$ wget ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020601/ERR2020601.fastq.gz

## if you don't have wget, you can instead use 'curl' with the command below.
# curl -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020601/ERR2020601.fastq.gz

## Then to check if the file is now in our working directory
$ ls

```

Great, the file is there! Now it's time for organising. We should move our 
fastq file into our newly created directory. This time, we can use `mv` the 
way it was meant to be used.

```bash
$ mv ~/ERR2020601.fastq.gz ~/BareBonesBash
$ ls
```

You should now see that the fastq file is no longer in your home folder. 
Let's go find it!

```bash
$ cd ~/BareBonesBash
$ ls 
```

Good, the file arrived in `~/BareBonesBash` safely! Maybe now would be a good 
time to check if we downloaded the right thing. In bash, you can normally use 
`cat` with text files, short for con**cat**enate, which is used to print the 
contents of a file to the screen. Lets try this with our newly downloaded file.

**BONUS TIP TIME!** If you're anything like Thiseas, who gets triggered at slow 
computer things, and prefer to have the computer do the work for you - try 
typing a couple of characters then press the "TAB" key on your keyboard.

```bash
$ cat ERR2020601.fastq.gz

```

Yay for auto-complete! But you probably had a bunch of junk printed to screen.
_[Looks like curiosity killed the `cat`! ]_

<p align="center"><img title="Source: https://giphy.com/gifs/kQbMO5X7UA1C8" src="https://media.giphy.com/media/kQbMO5X7UA1C8/giphy.gif" width="20%"></p>

That's because the FASTQ file, as with almost all FASTQs, is compressed (as 
indicated by the .gz). To view the _human readable_ contents of the file, we 
can instead use `zcat`. Don't forget your auto-complete!

```bash
$ zcat ERR2020601.fastq.gz

```

That looks much better, we can now actually see some DNA sequences! But you 
may have also noticed that a lot of stuff zipped past without you being able 
to see it. You could try scrolling but likely you'll not be able to go back 
far enough to see your previous commands. 

**BONUS TIP TIME!** try pressing `ctrl+l`, which will clear your terminal of 
all the junk that was printed to your screen. This does NOT delete those lines, 
it simply scrolls down for you. You can still find all your previous work if
you scroll up.

Now it's time for the inevitable tangent when your tutor thinks of a very 
(un)funny metaphor to explain something! _\[James added that and I didn't 
notice till it was too late >.<]_

## Asking the computer for help (it loves helping people)

As we just learned, the FASTQ file we've been playing with is compressed, 
_Zipped_, if you will. We constantly compress files in multiple different ways, 
but **why?** As the name suggests, compression saves disk space, so we can have 
more files stored on our system. 

An everyday example of the benefits of compression comes from music. To keep the 
calculations smaller we'll take a time machine back to 2001, when having one of 
these things made you instantly popular and better geared than James Bond _\[tech-savvy 
Pierce Brosnan, not the trigger-happy Daniel Craig]_:

<p align="center"><img title="Source: https://everymac.com/systems/apple/ipod/specs/ipod.html" src="https://everymac.com/images/cpu_pictures/apple_ipod.jpg" width="20%"></p>

That amazing piece of technology came with a storage space of 5GB, while an 
uncompressed music album takes up 640MB of space. **THAT IS 7.8125 ALBUMS!** 
At 20 songs per album, that makes less than 160 songs total! _"But my iPod had 
800 songs in it, and still had space!"_ I hear you thinking. That's mp3 
compression for you. Compression programmes you might be familiar with are, 
for example, WinZip or WinRar. 

Is there some way we could work out how much space we are saving by compressing
this FASTQ file? Let's ask the computer to help us find a way! The first command 
to use here is `whatis`, which will give a one line explanation of what a certain
command does. The second command we need is `man`. Using `whatis` we can find out
what `man` does.

```bash
$ whatis man

```

This will inform us that `man` is 
`an interface to the on-line reference manuals`. Cool! Now try to get 
information on `zcat` using `man`.

```bash
$ man zcat

```

This will open the manual page for `zcat` in a separate screen, which you can 
exit by pressing "`q`" on your keyboard. You can scroll up or down with the 
arrow keys. At the top of the screen you will see the command the manual is 
for, in this case it should read `gzip`. That is because `zcat` is part of the 
programme `gzip`. You will see a long description of the programme, followed by 
(scroll down) a section with all the options available. 

Isn't this great! The option `-l` lists the size of a file in both compressed 
and uncompressed form, as well as the compression ratio (how effective the 
compression was). **Most programmes you will use DO have a `man` page, making 
this command extremely useful.**. Now that we learned about the `-l` option of 
`gzip`, let's use it to see how efficient the compression of this FASTQ file is. 
_**\[Say it with us: "`man` is love. `man` is life."]**_


```bash
$ gzip -l ERR2020601.fastq.gz

```

A compression factor of `74.9%` is pretty good. It means our compressed FASTQ file is 
25.1% the size of the uncompressed file would.

## The Lord of the Pipes: One command to do them all.

After that tangent, let's get back to our regularly scheduled program(ming)!

We will now try out three semi-related commands to make viewing the contents 
of a file easier, and begin to familiarise with the most important 
functionality of bash: the concept of `|` (a.k.a. the "pipe"). 

<p align="center"><img title="Made with EZGif.com" src=".gifs/Boromir.gif" width="40%" height="10%"> <img title="Source: https://tinynin.wordpress.com/2012/01/08/marioportal-warp-pipe/" src="https://tinynin.files.wordpress.com/2012/01/warppipe-copy.gif" width="20%"></p>

A pipe passes the output of one command and gives it as input to the next. It 
allows us to string commands together, one after the other, which means you can 
do more complicated (and beautiful) things to your files "on the fly". The command
`head` allows you to view the first 10 lines of a file, while `tail` will show 
the last 10 lines. 

We will now print the file to screen with `zcat`, but rather than just let 
the whole thing print, we will "pipe" the output into `head`, which will 
allow us to see just the first 10 lines.

```bash
$ zcat ERR2020601.fastq.gz | head

```

We can also display more lines with the `-n` flag (short for "**n**umber of 
lines"). To see the first 20 lines you would use 

```bash
$ zcat ERR2020601.fastq.gz | head -n 20

```

The same option exists for tail, note that but options are not universal! Not 
every programme will use the same options!

```bash
$ zcat ERR2020601.fastq.gz | tail -n 4

```

And you can also chain them altogether _\[not unlike a human centipede... No 
gif here so we don't get fired]_

```bash
$ zcat ERR2020601.fastq.gz | head -n 20 | tail -n 4

```

The above command will print the whole file, but capture only the first 20 
lines, before printing out the last 4 lines of these 20.

<p align="center"><img title="Made with EZGif.com" src=".gifs/frodo.gif" width="30%" height="20%"></p>

In practice, what was just printed on your screen is the record of a single read, 
which spans 4 lines of the FASTQ file. 
* The record begins with the read ID, preceded by an `@`. 
* The next line contains the sequence of the read. 
* The third line is a separator line ('`+`'). 
* Finally, the fourth line of this record contains the base quality score for each 
position on the read, encoded a certain way. 
We won't go into the specific encoding of base quality scores here, but it is easy 
enough to find information about it online, if you want to know more. 

But what if you wanted to view the whole file "at your own leisurely pace"

<p align="center"><img title="Source: https://giphy.com/gifs/stroll-82abB3W2DknkY" src="https://media.giphy.com/media/82abB3W2DknkY/giphy.gif" width="20%"></p>

We can use the tool `less`, which prints the file to screen, but allows you 
to move up and down the output with your `arrow keys`. You can also move down 
a full screen with the `spacebar`.

```bash
$ zcat ERR2020601.fastq.gz | less

```

You can quit by pressing "q" on your keyboard.

Now we've had a look inside and checked that the file is a pretty normal FASTQ 
file, lets start asking more informative bioinformatic questions about it. A pretty 
standard question would be, **how many reads are in this FASTQ file?** We know 
now that each read record in a FASTQ file has four components, and thus takes 
up 4 lines. So if we count the number of lines in a file, then divide by four, 
we can work out how many reads are in our file. 

<p align="center"><img title="Source: https://giphy.com/gifs/l41YtZOb9EUABnuqA" src="https://media.giphy.com/media/l41YtZOb9EUABnuqA/giphy.gif" width="20%"></p>

For this we can use 'wc', which stands for "**w**ord **c**ount". However, we 
don't want to count words, we want to count the number of lines. We can 
therefore use the flag `-l` (try using what we learnt about `man` above to find lists of 
these flags!). But remember we first have to decompress the lines we are 
reading from the file with `zcat`.

```bash
$ zcat ERR2020601.fastq.gz | wc -l

```

This should give us 18880, which divided by four (since there are four lines 
per read), is 4720 reads.

Next, maybe we want to know what the name of each read is. When we used
`less` above, we saw each read header began with "@". Maybe we can use this
to our advantage!

<p align="center"><img title="Source: https://giphy.com/gifs/season-16-the-simpsons-16x3-3orieUe6ejxSFxYCXe" src="https://media.giphy.com/media/3orieUe6ejxSFxYCXe/giphy.gif" width="20%"></p>

The command `grep` will only print lines in a file that match a certain 
pattern. So for example, we want to search for every line in our FASTQ file 
that contains a '@'. Lets try it out again in combination with `zcat` and 
our pipes.

```zcat
$ zcat ERR2020601.fastq.gz | grep @

```

Unfortunately we seem to have picked up some other stuff because of the @ 
characters in the base quality lines. 

We can make our "pattern", in this case `"@"`, to be more specific by adding 
"ERR" to it. But let's also avoid flooding your screen with 4720 lines of 
stuff, and pipe that output into `less`, so we can look at it more carefully.

```zcat
$ zcat ERR2020601.fastq.gz | grep @ERR | less

```

Remember to press "q" to exit.

And for one final recap, we previously calculated there to be 4720 reads in our 
file. If we have just extracted the unique read _headers_ for every read, then 
in principle we can also just count these with `wc`!

```zcat
$ zcat ERR2020601.fastq.gz | grep @ERR | wc -l

```


<p align="center"><img title="Source: https://giphy.com/gifs/cheer-cheering-11sBLVxNs7v6WA" src="https://media.giphy.com/media/11sBLVxNs7v6WA/giphy.gif" width="20%"></p>

## Now you're thinking with portals! Symlinks and their usefulness.

The FASTQ we have been working with so far was downloaded from the ENA. It is 
important to keep the file name intact, so we can easily identify this specific 
FASTQ file in the ENA database in the future, if need be. 

In order to retain the original file, but also to play around with the 
contents, we can use a _symbolic link (**symlink**)_. You have doubtless seen 
these many times right on your desktop, in the form of desktop shortcuts! They 
are small portals that let you go to a remote location really fast, and take 
something from there. 

Imagine if you could reach the TV remote from the sofa, although for some 
strange reason you left it in the freezer when picking up the (now 
half-melted) ice cream. _\[No, of course Thiseas has never done that!]_

<p align="center"><img title="Source: https://ritorical.deviantart.com/art/Poor-messing-with-a-portal-gun-GIF-501341055" src="https://orig00.deviantart.net/784b/f/2014/354/a/3/poor_messing_with_a_portal_gun__gif__by_ritorical-d8ahh8f.gif" width="20%"></p>

So let us make a new subdirectory to store our symlink to the FASTQ file we 
already downloaded, and move to that directory.

```bash
$ mkdir ~/BareBonesBash/FastQ.Portals
$ cd ~/BareBonesBash/FastQ.Portals

```

It is now time to make the symlink. We do this with the `ln` command (short for 
"**l**i**n**k"), by providing the `-s` option, which specifies we want to create 
a **s**ymbolic link (i.e. a shortcut).
Note: You should give _absolute_ paths to the file your symlinks point to, or 
things **will** break down. (Note that a path that starts with `~` is technically 
an absolute path, since it is also not relative to your current position.)

```bash
$ ln -s ~/BareBonesBash/ERR2020601.fastq.gz .

```

Make sure you included that `.` in the command above. As discussed in the 
"Relative Paths" section, that points your current working directory, thus 
telling the `ln` programme that it should create the link in the current 
directory. You should now see the symlink in the directory. 

<p align="center"><img title="Source: https://imgur.com/gallery/GOyDQjn" src="https://78.media.tumblr.com/0ac8df83e4b5ee82c150048347a7db01/tumblr_n1blyfhvTY1qfbz1so1_500.gif" width="30%"></p>

To see where the link points to we can use `ls -l`, which provides exended 
information on the files shown with `ls`. (For more information you can look 
at the `man` page for `ls`).

```bash
$ ls -l

```

We can now look at the original FASTQ file by using our symlink. Note 
that while command looks the same as in the section above, we are in a 
different directory, so the `ERR2020601.fastq.gz` _here_ is technically 
different to the original. It is now a shortcut to the originl file, which 
happens to have the same name. So, repeating above:

```bash
$ zcat ERR2020601.fastq.gz | head -n 20 | tail -n 4

```

Which should print out the same read as it did on the original FASTQ file.

## Lazyness 101: Minimising our work by maximising the work of the computer

### Text Editing in Terminal

Now for a bit of honesty. A single sample will not get you a nature publication.
_\[ok, maybe sometimes]._ We will need more data if we're gonna make it to the
most prestigious journals. So let's download another 7 samples from James' 
Mammoth project to get us on our way to a nature cover page. (See [here](https://www.ebi.ac.uk/ena/data/view/PRJEB21582) for the ENA page of the project) _[Yay! Free Publicity!]_.

It is a lot of work to run `wget` 7 times while changing the command everytime.

**Bonus tip time!** One way would be to press the 'up' arrow on your keyboard,
which will allow you to scroll through all your previous commands. Thus you 
could pull up the previous command, then just change a couple of characters.
This can be useful in certain cases, but doing that 8 times is **still** too 
much work.

Good thing we're here to learn how to be lazy! We can download multiple files 
from an ftp server by giving `wget` a file that contains the ftp links for each 
file we want downloaded. 

But how can we make this file? There are multiple options for text editing in
the terminal. If you're absolutely insane you may look up `vim` 
_\[Thiseas' poison]_, or we can use `nano` which is much more user friendly. 

Editing the contents of a file in `nano` is mostly as you would with your 
standard `TextMate` or `gedit` on your local machine. However, the main 
difference is how you save, and close the program which you perform using 
keyboard combinations (like you would use `ctrl + c` to copy a line in your 
typical 'Microsoft Office' suite).

So open up the program with

```bash
$ nano

```

And you will now see a blank window, with a section at the bottom with 
a variety of commands at the bottom (where `^` corresponds to the `ctrl` or 
`cmd` key on your keyboard). You can try typing and deleting text as you 
normally would on your offline text editor, moving around the page with your 
arrow keys.

To save the contents of the file, we want to begin by initating our exit
with `ctrl+x`. At the bottom you will be prompted to "Save modified buffer", 
press `y` on your keyboard to agree. Now you will be asked what you want 
the file to be called. Type `~/BareBonesBash/Ftp.Link.txt` to give both
the directory and the file name (`Ftp.Link.txt`), and then press `enter`.

We can check that the file was successfully generated by navigating into 
the directory and doing `ls`.

```bash
$ cd ~/BareBonesBash/
$ ls

```
Great! There is a file there! But wait! OH NO! There is another typo! We 
have multiple _links_ not a Link!

<p align="center"><img title="Source: https://giphy.com/gifs/the-legend-of-zelda-link-funny-RkymcOKhoCRTG" src="https://media.giphy.com/media/RkymcOKhoCRTG/giphy.gif" width="30%"> <img title="Source: https://giphy.com/gifs/link-the-legend-of-zelda-NVBR6cLvUjV9C" src="https://media3.giphy.com/media/NVBR6cLvUjV9C/giphy.gif" width="30%"><br /><i>[Dear lord, how much nerdier can we get here -.- ...]</i></p>

Lets remove that file, and start again. 

So far, we learnt `rmdir` to remove a directory. To remove a file, we can
instead use `rm` for – you guessed it! – **r**e**m**ove. 

```bash
$ rm Ftp.Link.txt
$ ls

```
And it's gone!

You can also use `rm` to remove directories using it with the flag `-r`,
but this is 'less' safe - **it will not warn you if a directory has stuff
already inside it.**

Anyway, lets start again, but this time get ready to download our extra 
Mammoth files, using our relative paths to go back to our home directory,
and opening up `nano` again

```bash
$ cd ~
$ nano

```

Copy the text below into the blank window, as you would normally when at 
your terminal command prompt (`cmd+v` on OSX or `ctrl+shift+v` on Linux).

<pre>
ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/009/ERR2020609/ERR2020609.fastq.gz
ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020611/ERR2020611.fastq.gz
ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/007/ERR2020567/ERR2020567.fastq.gz
ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/005/ERR2020565/ERR2020565.fastq.gz
#ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020601/ERR2020601.fastq.gz
ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/003/ERR2020613/ERR2020613.fastq.gz
ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/008/ERR2020618/ERR2020618.fastq.gz
ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/007/ERR2020617/ERR2020617.fastq.gz
</pre>

(Note the `#`, this is **commented out** as we've already downloaded this file!)

So again to recap exiting and save a file in nano we do the following dance: 
* to initate exit: `ctrl+x`
* Press `y` to say you want to "Save modified buffer", 
* Type the file name`~/BareBonesBash/Ftp.Links.txt` and then press `enter`.

To verify that it worked correctly, we can either use the command that we 
learnt above to print to screen the contents of the file (which is...?), or
we can use `nano` again, but with the file as an argument to open the 
file and see the contents.

```bash
$ nano ~/BareBonesBash/Ftp.Links.txt

```

This time when you exit with `ctrl+x` you'll immediately return to your 
command prompt, as you made no changes to the file.

Woop! Now lets utilise the file we just created, by downloading all the files
stored in the URLs. IN ONE GO! 

<p align="center"><img title="Source: https://giphy.com/gifs/aliens-oAEoEC7vdf1QI" src="https://media.giphy.com/media/oAEoEC7vdf1QI/giphy.gif" width="30%"></p>

You can provide a file to `wget` with URLs (like the one you just made) using 
the flag `-i`, for "**i**nput". 

```bash
$ cd ~/BareBonesBash
$ wget -i ~/BareBonesBash/Ftp.Links.txt

## curl cannot handle links from a file, so if you are using curl, you should run the command below to download all the files.
#  curl -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/009/ERR2020609/ERR2020609.fastq.gz -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020611/ERR2020611.fastq.gz -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/007/ERR2020567/ERR2020567.fastq.gz -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/005/ERR2020565/ERR2020565.fastq.gz -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/003/ERR2020613/ERR2020613.fastq.gz -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/008/ERR2020618/ERR2020618.fastq.gz -O ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/007/ERR2020617/ERR2020617.fastq.gz

```

Look at that! One command instead of 7! You're becoming a bash pro already! 

### What is a Variable anyway?

Time for another tangent! You will now learn the `echo` command. 
In bash `echo` just prints things. The name refers to the fact that since the 
computer "says" what you just told it to say, it behaves like an echo of yourself.
Tradition dictates that the first thing you have the computer say in programming 
tutorials is "Hello World!", so here goes:

```bash
$ echo Hello World!

```

Great! Now back to the question at hand. What _is_ a variable anyway? That is a good 
question! A variable is something that changes! But what does that mean, exactly? A 
variable can be "set" (i.e. telling the computer what that variable means) to a 
variety of things. Some variables are set _for_ you, the moment you open your terminal 
or log into a servers. By convention, such variables have names in ALL CAPS. An example 
of such a variable is `HOME`, which stores the location of your home directory. Therefore, when you use the shorthand `~`, the 
computer looks into that variable to see what that means. However, the computer 
cannot always tell what is a variable and what is just text. It relies on you to 
tell it what should and should not be "unpacked". "Unpacking" means "telling the 
computer to look at what is _inside_ a variable. We signal the computer that we wish 
to look inside a variable by using the `$` character in front of the variable name. 
Try this:

```bash
$ echo HOME    #This will print the word HOME.
$ echo $HOME   #This will print the contents of the variable HOME.

```

Variables as the one above are called **environment variables** and should generally 
**NOT** be changed on a whim _\[even though the temptation might be a whim away. A 
whim away... A-whim-away...]_.

<p align="center"><img title="Source: http://en.webfail.com/e91115df851" src="http://cdn.webfail.com/upl/img/e91115df851/post2.jpg" width="30%"></p>

But you can also set your own variables, which is extremely handy. Any variable can be easily 
overwritten, which is one reason why they are so useful. Therefore, as long as you don't 
give your variables names in ALL CAPS, you won't run the risk of overwriting environment 
variables, and everyone is happy. One way to assign variables is by using an `=`. In the 
example below, we will set and overwrite the variable `GreekFood`, and then "unpack" it in 
several sentences _\[which also happen to be objectively true\]_.

```bash
$ GreekFood=4            #Here, 'GreekFood' is a number.
$ echo "Greek food is $GreekFood people who want to know what heaven tastes like."
#
$ GreekFood=delicious   #Now we overwrite that number with a word (or a "string" of characters).
$ echo "Everyone says that Greek food is $GreekFood."
#
$ GreekFood="Greek wine" #We can overwrite 'GreekFood' again, but when there is a space in our string, we need quotations.
$ echo "The only thing better than Greek food is $GreekFood!"
#
$ GreekFood=7 #And, of course, we can overwrite with a number again too.
$ echo "I have been to Greece $GreekFood times already this year, for the food and wine!"
#

```

<p align="center">
  <img title="Source: http://visitgreece-gr.tumblr.com/" src="https://78.media.tumblr.com/04ac7d0699ac494a7ccb4fc9316bbc0a/tumblr_oo77m9RLgv1uwr1s7o1_500.gif" width="30%">
</p>

We will talk about quotes another time, so just forget you used them for the 
moment :wink:.

Now you have a basic understanding of Greek food. I mean **variables** in bash! Let's see 
how we can use this knowledge.

### Loop de Loop

Now to minimise our workload in making the symlinks for all the FASTQ files we downloaded 
previously! We can do this using a **for loop**, one of the basic methods of all programming. 

Imagine you have to order pizzas for a varying number of scientists every week. 
_\[Just a random example]._ For every person you will need an extra pizza. This 
is a sort of "for loop": whereby you go through the list of names of hungry 
scientists, and you add one more pizza to the list for every name. Note that the 
specific names of the scientists wouldn't really matter here, only the number of 
names. So in pseudocode (code-like writing that is human readable but a computer 
will not understand it), the above loop would look like this:

```
## Don't copy and paste this, it will not work.
for every scientist:
  Order another pizza
done
```

<p align="center"><img title="Source: https://tenor.com/view/izza-oprah-eatwhatyouwant-gif-4149888" src="https://media1.tenor.com/images/5ef4336be26e478431f85b349ec6bd34/tenor.gif?itemid=4149888" width="20%"></p>

Let's stop daydreaming of pizza now and return to the task at hand. For each FASTQ 
file we want to make a symlink to that file. 

Lets first check this will work as we expect by converting our pseudo-code to 
real code, but getting the computer to TELL us what it says we have told it 
what to do (with actually doing it), by putting the command in `echo`!

```bash
$ for fastq in ERR2020609.fastq.gz ERR2020611.fastq.gz ERR2020567.fastq.gz ERR2020565.fastq.gz ERR2020613.fastq.gz ERR2020618.fastq.gz ERR2020617.fastq.gz; do 
>    echo "ln -s ~/BareBonesBash/$fastq ~/BareBonesBash/FastQ.Portals"
> done
```

Look! You can see all the hard work of typing you DON'T have to do! Woohoo!

So try removing the echo and see what happens.

```bash
$ for fastq in ERR2020609.fastq.gz ERR2020611.fastq.gz ERR2020567.fastq.gz ERR2020565.fastq.gz ERR2020613.fastq.gz ERR2020618.fastq.gz ERR2020617.fastq.gz; do 
>  ln -s ~/BareBonesBash/$fastq ~/BareBonesBash/FastQ.Portals
> done
```

After writing the first line, and pressing enter, you may have noticed how 
the prompt changes from `$` to `>`. This means that your command still expects 
more information before it can execute! In this case it is completed when 
`done` is encountered. (If you accidently get stuck there and can't leave, 
press `ctrl + z` on your keyboard).

Once you've written done - lets see if the command worked correctly!

**Bonus tip time!** `ls` will also accept a particular path to print to screen. 
i.e. If you're in a different directory but want to see the contents of a 
different one, you can follow the example here, where we are in `~/BareBonesBash`
but want to check the contents of `FastQ.Portals/` 

```bash
$ ls -l FastQ.Portals/

```

Going back to our loop - the above example `fastq` (case-sensitive) is 
**the variable**. In this case it is set to a **string** of characters, 
corresponding to the name of the first FASTQ file (`ERR2020617.fastq.gz`). 
At that point the command given within the loop (in this case `ln -s`) is 
executed, before the next FASTQ. After it has completed, the next file in the 
list (`ERR2020611.fastq.gz`) is picked up, and the loop is repeated. 

Described in more pseudocode:

```
for every_object in a_list; do
  <this_command> on <this_object>
done
```

It is important that you separate out your 'loop' from the command itself using
`; do`, and finish the loop with `done`, otherwise bash will keep waiting for
some other input.

In the loop we just performed, we want to use what is in the `fastq` variable, 
to tell the computer what to perform `ln` on. To tell the computer what to use 
in `fastq`, we prefix `$` to the variable name.

This means that when reading `~/BareBonesBash/$fastq`, the computer knows that 
`$fastq` means "use what ever is stored in the variable `fastq`", thus seeing 
`~/BareBonesBash/ERR2020609.fastq.gz`. 

In the second part of the command (`~/BareBonesBash/FastQ.Portals`), there is 
no `$` in front of the sequence of letters `FastQ`. In this case the computer 
reads it as the letters themselves and not the contents of a variable 
(which is what we wanted to happen). The word is also in written in a different 
case, so it would **NOT** be read as the variable even with the `$` character. 

See the example below for more info:

```bash
$ echo -e "$FastQ <---- Not a set variable"
$ echo -e "$fastq <---- The last FastQ file in the list of files in the loop."

```

However, this not the only way to write a loop. In the loop we ran above, we 
still had to do a lot of writing; writing out the name of every file. But worry 
not, this is Lazyness 101, and here we like to **NOT** write a lot! It is our 
_right_ not to type more than we need to! It is therefore our right - nay, 
our _responsibility_ - to use **wildcards** "refers to a character that can be 
substituted for zero or more characters in a string". In bash, the wildcard 
character is the asterisk (`*`) 
_\[Not to be confused with Asterix, James. AGAIN, REALLY!?)]_. 

<p align="center"><img title="Source: https://www.garethjmsaunders.co.uk/2008/01/29/asterix-and-asterisk/" src="https://www.garethjmsaunders.co.uk/wp-content/uploads/2008/01/asterix_or_asterisk.gif" width="30%"><br /><i> [Take note James...] </i></p>

For example, we could remove (using `rm` as we learnt above) any object with any 
combination of characters in it's name, with the following command. But we _won't_ 
do that.

```bash
# rm ~/BareBonesBash/FastQ.Portals/*
```

In the context of a loop, we can use the wildcard to tell bash the loop 
should be performed on ALL items in a directory that match the criterion given. 
If we want to create a symlink (with `ln -s`) for every item within the 
`~/BareBonesBash` directory, and place that symlink within the 
`~/BareBonesBash/FastQ.Portals` directory, we could use: 

```bash
$ for fastq in ~/BareBonesBash/*; do
>  ln -s $fastq ~/BareBonesBash/FastQ.Portals
> done

```

If you need to be more specific with your loop, you can also use the wildcard
with some other characters. For example, `ERR*` would mean perform a command on
every file that begins with ERR, regardless of what comes after ERR. Finally, 
we can use characters AFTER the wildcard as well, to only pick up files that have 
a certain suffix as well as prefix (e.g. `ERR*.gz` will find all files that begin 
with `ERR` and end with `.gz`, regardless of what (if anything) comes between the 
two).

For example, lets try out one of our old commands in a loop. Lets use 
`gzip -l` on every file starting with `ERR` and ending with `.gz` in our 
new directory.

```bash
$ for fastq in ~/BareBonesBash/ERR*.gz; do
>  gzip -l $fastq
> done

```

Therefore, loops and wildcards allow us to do repetitive tasks, and reap the 
rewards thereof, without having to do all the repetitive work! 
<p align="center"><img title="Source: https://giphy.com/gifs/tinder-automation-tinderbot-3rgXByefj5zvCcodOM" src="https://media.giphy.com/media/3rgXByefj5zvCcodOM/giphy.gif" width="40%"></p>

As a final practice, have a look inside your `~/FastQ.Portals` directory. You 
might notice that you have also symlinks to `FastQ.Portals` and `Ftp.Links.txt`
as well as our FastQ files. These came in our previous `ln -s` loop, as we 
used the wildcard for _everything_ in `~/BareBonesBash`. 

Try writing your own loop using `for`, `*`, and `rm` to remove ONLY those 
two files.

## The road so far

Thank you for joining us in this small tutorial, and for putting up with our 
terrible pop-culture and video game references. All in all, you should now know 
how to move around using the Terminal, as well as the basic commands you need to
create, view and manipulate files and directories.

We are planning a second part of this tutorial series, with slightly more advanced
tricks, to ensure using bash doesn't make you feel... __BASHED__!


<p align="center"><img title="Source: https://giphy.com/gifs/csi-miami-horatio-caine-xPGkOAdiIO3Is" src="https://media1.giphy.com/media/xPGkOAdiIO3Is/giphy.gif" width="30%"> <img title="Source: https://giphy.com/gifs/swag-80s-sunglasses-62PP2yEIAZF6g" src="https://media.giphy.com/media/62PP2yEIAZF6g/giphy-downsized.gif" width="40%"></p>
  
Please let us know if you have feedback or if there are any questions, don't 
be... __BASHFUL__! 

_\[I'll see myself out...]_

----

## _OPTIONAL:_ The Cleanup Crew
It is extremely important to ALWAYS keep your directories clean from random clutter. This lowers
 the chances you will get lost in your  directories, but also ensures you can stay lazy, since TAB 
completion will not keep finding similarly named files. So let's clean up your home directory by 
removing all the clutter we downloaded and worked with today. The command below will remove the 
`~/BareBonesBash` directory **as well as all of its contents**. 

```bash
$ cd ~     # We shouldn't delete a directory while we are still in it. (It is possible though).
$ rm -r ~/BareBonesBash
```

<p align="center"><img title="Source: https://i.imgur.com/lcxyE0D.gif" src="https://i.imgur.com/lcxyE0D.gif" width="40%"></p>

----

## For next time!

We will learn about:
* advanced echo
* double and single quotes (or in grep and loops)
* rev
* cut
* find
* awk
* sed
* parallel
* while loops
* if statements
* bash arithmetic "$((8*8))"
 
