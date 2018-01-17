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

<img src="https://media.giphy.com/media/3o84U72tKO389H2lI4/giphy.gif" width="20%">

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
  or two (`../`) dots followed by a forward slash, **but not always**. In the 
  syntax of relative pathways `.` means "the current directory" and `..` means 
  "the parent directory". 

As a real life example, imagine you are walking down the street when a car 
stops to ask for the way to the Brandenburger Tor. You could tell them how to 
get to the Tor from Ethiopia (since that is the presumed root where all humans 
started their journey) _\[haha, human history joke]_, or you could say "Take 
a left here, straight for 3 blocks, and you're there.". The latter set of 
directions is relative to their current position, while the first one is not.

<img src="https://media.giphy.com/media/3o6Ztk4xTVAnfqYPn2/source.gif" width="20%"> <img src="https://media.giphy.com/media/QWXhaNjfwuNs4/source.gif" width="20%">

Now let's look around at out current location and see what we can find withing 
our home directories. We can use the command `ls`, shorthand for "list", which 
will (surprise surprise) list the directory contents.

```bash
ls
```

Your home directory should come equipped with multiple subdirectories like 
"Documents", "Pictures", etc. 

It is now time to start moving (navigating) towards "the Brandenburger Tor" 
from the example above. We can navigate through directories using the command 
`cd` which stands for "**c**hange **d**irectory".

```bash
cd Documents/
```

This command will move you from your home directory to its "Documents" 
subdirectory. Note that `Documents/` above is indeed a relative path, since it 
starts from the home directory (the initial `./` is implied). To find the 
absolute path of the "Documents" directory we will once again use `pwd`.

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
use a dash (`-`), to indicate 'my previous location'. This is useful since you
 can move multiple directories with one `cd` command. So, now, to return to our 
home directory from the documents directory we can type:

```bash
cd -
pwd
```

And voilá! We are back in our home directory.

However, often when working in bioinformatics we will be working remotely on a 
server. The most typical way is to log in via "**s**ecure **sh**ell", known as 
`ssh`. Note that you can normally only log into an institute's server being on 
the network of the institute and or via VPN, so make sure are on either of 
those.

A typical `ssh` command consists of the `ssh`, with a user, '@' symbol and then 
the address of the server. For example:

```bash
ssh <user>@<my>.<address>.com
```


---

**MPI-SHH ONLY**
For example we can log into SDAG with the following, replacing <username> with 
your username. Note that this will normally ask you for your password.

```bash
ssh <user>@mpi-sdag1.sdag.ppj.shh.mpg.de
```

---

Once we've logged in the `~` points to a different home directory, as you are 
on a different machine. However, all of the commands you've learned so far will 
still work the same. ;)

It is important to keep your corner of the servers well organised, and the 
trick to doing that is making your own directories. Often _a lot_ of them. 
You can make a new empty directory using the command `mkdir`, shorthand for 
"**m**a**k**e **dir**ectory".

```bash
mkdir ~/BareBonesBosh
ls ~
```

You can now see your new and devoid-of-content directory. But don't celebrate 
yet! The directory has the wrong name! Who could have seen _this_ coming? If 
you saw the typo and fixed it already, no brownies for you! But don't lose 
hope, because we can rename things with the `mv` command, shorthand for "move". 

In fact move, as the name suggests, will move a file/folder into a new location, 
also renaming it in the process, if necessary. It works by `mv`, the old 
location and a target location.

```bash
mv ~/BareBonesBosh ~/BearBonesBash
```

The command above will now move the directory into the same location, but with
the target location having a different name, essentially renaming it to 
`BearBonesBash`. 

But oh no! Not again! This is not a bash tutorial for ancient bear genomics! 
Let's just delete that empty directory and start over, using the `rmdir` 
command, short for "**r**e**m**ove **dir**ectory".

```bash
rmdir ~/BearBonesBash
ls ~
```

And now we can create our directory, properly named this time, and move into it.

```bash
mkdir ~/BareBonesBash
cd ~/BareBonesBash
```

## Playing with files




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
* download more files from ENA with a provided list.
* small for loop to copy and rename the rest of the fastq.gz with ln -s.

## "Help" - The Beatles

* whatis
* man

## DIE ZUKUNFT

* find
* awk
* sed
* parallel
* bash arithmetic "$((8*8))"
* double and single quotes (or in grep and loops)
 
