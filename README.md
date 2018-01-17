# BareBonesBash
A basic Bash tutorial by @jfy133 and @TCLamnidis.

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

## Introduction

The aim of this tutorial is to make you familiar with using bash everyday... 
for the rest of your life. More specifically, we want to do this in the context
of our work. We will start with how to navigate (Thiseas' words...) around a 
filesystem in the terminal, download sequencing files, and then to 
manipulate these. Within these sections we will also show you simple tips and 
tricks to make your life generally easier. In fact, some of these commands we 
only just learnt last week (thanks Aida!) and we've been using the terminal 
for more than 2 years.

This tutorial is designed to be self sufficent using public data. Thus you
can do this anywhere on any PC with a unix terminal (no warranty provided).

## Navigating the maze

After opening the terminal what you will normally see is a blank screen with a
'command prompt'. This typically consists of your username, device name a colon, 
a directory path and ends with a dollar symbol. Like so.

```bash
<username>@<device_name>:~$
```

Note that prompts _are_ customisable, so will not always be displayed as above 
(look at Thiseas' magical prompt as an example. James keeps his vanilla as he 
is a barbarian).

The prompt is never involved in any command, it is just there to help you know
who and where you are. Therefore you must always make sure when copying a 
command (see later) that you do **NOT** include the prompt.

Here, the directory `~`, stands for your home directory. This shorthand can be 
seen and used both on your machine and on the cluster. Note that this shorthand 
will point to a different place, depending on the machine and the user.

If you want to know what the shorthand means, (here comes your first command!)
you can type in `pwd`, which is short for "**p**rint **w**orking **d**irectory". 
The working directory stands for whichever directory you are currently in. 

```bash
pwd
```

There are two types of filepaths: 
* An **Absolute** path will start with the deepest directory in the machiene, 
  shown as a `/`. That is the directory path you see in the output of the `pwd` 
  command you just ran.
* Alternatively a relative path always begins from your working directory (i.e.
  your current directory). Often this type of path will begin with one (`./`) 
  or two (`../`) dots followed by a forward slash, **but not always**.

As a real life example, imagine you are walking down the street when a car 
stops to ask for the way to the Brandenburger Tor. You could tell them how to 
get to the Tor from Ethiopia (since that is the presumed root where all humans 
started their journey) \[haha, human history joke], or you could say "Take a 
left here, straight for 3 blocks, and you're there.". The latter set of 
directions is relative to their current position, while the first one is not.

It is now time to start moving (navigating) towards "the Brandenburger Tor". 
We can navigate through directories using the command `cd` which stands for 
"**c**hange **d**irectory".

```bash
cd Documents/
```

This command will move you from your home directory to its "Documents" 
subdirectory. Note that `Documents/` above is indeed a relative path, since it 
starts from the home directory. To find the absolute path of the "Documents" 
directory we will once again use `pwd`.

```bash
pwd
```

Now we can move up one directory, back to your home using the relative path
`../`.

```bash
cd ../
```

We can also change directories using absolute paths. Lets do this using the 
absolute path we printed using `pwd` in the previous step. Type `cp`, but don't 
press enter yet! Copy and paste the output of the previous `pwd` command 
(which you can see in your terminal does not have the command prompt), after 
the `cd`, then press enter.

For example:

```bash
cd /home/fellows/Documents
```

Now for one last move, here is a lesser-known trick. When using `cd` you can 
use a dash (`-`), to indicate 'my previous location'. So, now, to escape from 
the documents directory we can type:

```bash
cd -
pwd
```

And voilá! We are back in our home directory.




* ls
* ssh
* cd / pwd (recap)

* mkdir 
* mv to rename directory
* cd
* wget ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020601/ERR2020601.fastq.gz [217.2kb Mammoth mtCapture data]
* zcat
* pipe
* head/tail/less
* wc -l
* grep

preserve original file, so make symlink in new directory
* mkdir
* ln -s 
* mv (the symlink) ERR2020601.fastq.gz JK2781_MT.fastq.gz
* ls -l (to see)


## "Help" - The Beatles

* whatis
* man

## DIE ZUKUNFT

* find
* awk
* sed
* parallel
* bash arithmetic "$((8*8))"
