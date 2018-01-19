# BareBonesBash
A basic Bash tutorial by @jfy133 and @TCLamnidis.

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><p align="center"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

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

<p align="center"><img src="https://media.giphy.com/media/3o84U72tKO389H2lI4/giphy.gif" width="20%"></p>

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

<p align="center"><img src="https://media.giphy.com/media/3o6Ztk4xTVAnfqYPn2/source.gif" width="20%"> <img src="https://media.giphy.com/media/QWXhaNjfwuNs4/giphy-tumblr.gif" width="20%"></p>


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
press enter yet! 

<p align="center"><img src="https://media.giphy.com/media/23BST5FQOc8k8/source.gif" width="20%"></p>

Copy and paste the output of the previous `pwd` command 
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
you saw the typo and fixed it already, no brownies for you! 

<p align="center"><img src="https://media.giphy.com/media/ieGdB2g5kDIkg/giphy.gif" width="20%"></p>

But don't lose hope, because we can rename things with the `mv` command, 
shorthand for "move". 

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

<p align="center"><img src="https://media.giphy.com/media/IQ9KefLJHfJPq/giphy.gif" width="20%"></p>

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

## Playing with files, one bit at a time

So we have places to organise our files... buuut we don't have any files yet! 
Lets change that.

We ain't playing with bears today - that's dangeous (as we saw above), instead
lets play with some Mammoths!

<p align="center"><img src="https://media.giphy.com/media/kbuQOkATEo6VW/giphy.gif" width="20%"> <img src="https://media.giphy.com/media/3o6Zte5Q11lxAu8Q5q/giphy.gif" width="20%"></p>

We're going to use `wget` to download a FASTQ file from the ENA. So while in 
our `BareBonesBash` directory, we will give `wget` the link to the file, and 
we should see a loading bar. Once downloaded (it should be pretty quick),
we can use `ls` to check the contents.

<p align="center"><img src="https://media.giphy.com/media/lAIbbDbcXSZSU/giphy.gif" width="20%"></p>

```bash
wget ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020601/ERR2020601.fastq.gz
ls
```

Great! But maybe we want to check we downloaded the right thing. In bash,
with text files you can normally use `cat`, which is used to print the 
contents of a file to the screen. Lets try this with our newly downloaded file.

If you're anything like Thiseas, who gets triggered at slow computer things, 
and prefer to have the computer do the work for you - try typing a couple of 
characters then press the "TAB" key on your keyboard.

```bash
cat ERR2020601.fastq.gz
```

Yay for auto-complete! But you probably had a bunch of junk printed to screen.

<p align="center"><img src="https://media.giphy.com/media/kQbMO5X7UA1C8/giphy.gif" width="20%"></p>

That's because the FASTQ file, as with almost all FASTQs, is compressed (as 
indicated by the .gz). To then view the _real_ contents of the file, we can 
instead use `zcat`. Don't forget your auto-complete!

```bash
zcat ERR2020601.fastq.gz
```

That looks much better, we can now actually see some DNA sequences! But you 
may have also noticed that a lot of stuff zipped past without you being able 
to see it. You could try scrolling but likely you'll not be able to go back 
far enough to see your previous commands. 

Tip: try pressing `ctrl+l`, which will clear your terminal of all the 
junk that was printed to your screen. This does NOT delete those lines, 
it simply scrolls down for you. You can still find all your previous work if
you scroll up.

## Asking the computer for help (it loves helping people)
As we just learned, the FASTQ file we've been playing with is compressed. _Zipped_,
if you will. We constantly compress files in multiple different ways (bams are 
another example of a compressed file), but **why?** As the name suggests, 
compression saves disk space, so we can have more files stored on our system. 

An everyday example of the benefits of compression comes from music. To keep the 
calculations smaller we'll take a time machiene back to 2001 when having one of 
these things made you instantly popular and better geared than James Bond (tech-savvy 
Pierce Brosnan, not the trigger-happy Daniel Craig):

<p align="center"><img src="https://everymac.com/images/cpu_pictures/apple_ipod.jpg" width="20%"></p>

That amazing piece of technology came with a storage space of 5GB, whie an 
uncompressed music album takes up 640MB of space. **THAT IS 7.8125 ALBUMS!** 
At 20 songs per album, that makes less than 160 songs total! "But my iPod had 
800 songs in it, and still had space!" I hear you thinking. That's mp3 
compression for you. Compression programmes you might be familiar with are, 
for example, WinZip or WinRar. 

Is there some way we could work out how much space we are saving by compressing
this FASTQ file? Let's ask the computer to help us find a way! The first command 
to use here is `whatis`, which will give a one line explanation of what a certain
command does. The second command we need is `man`. Using `whatis` we can find out
what `man` does.

```bash
whatis man
```

This will inform us that `man` is `an interface to the on-line reference manuals`. 
Cool! Now try to get information on `zcat` using `man`.

```bash
man zcat
```

This will open the manual page for `zcat` in a separate screen, which you can exit 
by pressing "q". You can scroll up or down with the arrow keys.
At the top of the screen you will see the command the manual is for, in this case 
it should read `gzip`. That is because `zcat` is part of the programme `gzip`. You 
will see a long Description of the programme, followed by (scroll down) a section 
with all the options available. 
Isn't this lucky! The option `-l` lists the size of a file in both compressed and 
uncompressed form, as well as the comprassion ratio (how effective the compression 
was). **Most programmes you will use DO have a `man` page, making this command 
extremely useful.**
Now that we learned about the `-l` option of `gzip`, let's use it to see how efficient 
the compression of this FASTQ file is. 

```bash
gzip -l ERR2020601.fastq.gz
```
A compression factor of `74.9%` is pretty good. It means our compressed FASTQ file is 
25.1% the size of the uncompressed file would.

## The Lord of the Pipes: One command to do them all.

We will now try out three semi-related commands to make viewing the contents 
of a file, and begin to familiarise with the most important functionality of 
bash: the concept of `|` (i.e. the "pipe"). 

<p align="center"><img src=".gifs/Boromir.gif" width="40%" height="10%"> <img src="https://tinynin.files.wordpress.com/2012/01/warppipe-copy.gif" width="20%"></p>

A pipe passes the output of one command and gives it as input to the next. It 
allows us to string commands together, one after the other, which means you can 
do more complicated (and beautiful) things to your files "on the fly". The command
`head` allows you to view the first 10 lines of a file, while `tail` will show 
the last 10 lines. 

We will now print the file to screen with `zcat`, but rather than just let 
the whole thing print, we will "pipe" the output into `head`, which will 
allow us to see just the first 10 lines.

```bash
zcat ERR2020601.fastq.gz | head
```

We can also display more lines with the `-n` flag (short for "**n**umber of 
lines"). To see the first 20 lines you would use 

```bash
zcat ERR2020601.fastq.gz | head -n 20
```

The same option exists for tail (but options are not universal. not every 
programme will use the same options!)

```bash
zcat ERR2020601.fastq.gz | tail -n 4
```

And you can also chain them altogether (not unlike a human centipede...) _\[no 
gif here so I don't get fired]_

```bash
zcat ERR2020601.fastq.gz | head -n 20 | tail -n 4
```

The above command will print the whole file, but capture only the first 20 
lines, before printing out the last 4 lines of these 20.

<p align="center"><img src=".gifs/frodo.gif" width="30%" height="20%"></p>

In practice, what was just printed on your screen is the record of a single read, 
which spans 4 lines of the FASTQ file. 
* The record begins with the read ID, precceded by an `@`. 
* The next line contains the sequence of the read. 
* The third line is a separator line ('`+`'). 
* Finally, the fourth line of this record contains the base quality score for each 
position on the read, encoded a certain way. 
We won't go into the specific encoding of base quality scores here, but it is easy 
enough to find information about it online, if you want to know more. 

But what if you wanted to view the whole file "at your own leisurely pace"

<p align="center"><img src="https://media.giphy.com/media/82abB3W2DknkY/giphy.gif" width="20%"></p>

We can use the tool `less`, which prints the file to screen, but allows you 
to move up and down the output with your arrow keys. You can also move down a full 
screen with space.

```bash
less ERR2020601.fastq.gz
```

You can quit by pressing "q" on your keyboard.

Now we've had a look inside and checked that the file is a pretty normal FASTQ 
file, lets start asking more informative bioinformatic questions about it. A pretty 
standard question would be, **how many reads are in this FASTQ file?** We should all 
know now that each read record in a FASTQ file has four components, and takes up 4 
lines. So if we count the number of lines in a file, then divide by four, we can work
out how many reads are in our file. 

<p align="center"><img src="https://media.giphy.com/media/l41YtZOb9EUABnuqA/giphy.gif" width="20%"></p>

For this we can use 'wc', which stands for "**w**ord **c**ount". However, we 
don't want to count words, we want to count the number of lines. We can therefore use 
the flag `-l` to do this. But remember we first have to decompress the lines we are 
reading from the file with `zcat`.

```bash
zcat ERR2020601.fastq.gz | wc -l
```

This should give us 18880, which divided by four (since there are four lines per read), is 4720 reads.

Finally, maybe we want to know what the name of each read is. When we used
less above, we saw each read header began with "@". Maybe we can use this
to our advantage!

<p align="center"><img src="https://media.giphy.com/media/3orieUe6ejxSFxYCXe/giphy.gif" width="20%"></p>

The command `grep`, will only print lines in a file that match a certain 
pattern. So for example, we want to search for every line in our FASTQ file 
that contains a '@'. Lets try it out again in combination with `zcat` and 
our pipes.

```zcat
zcat ERR2020601.fastq.gz | grep "@"
```

Unfortunately we seem to have picked up some other stuff because of the @ 
characters in the base quality lines. We can make our "pattern", in this 
case `"@"` more specific by adding "ERR" to it. But let's also avoid flooding 
your screen with 4720 lines of stuff, and pipe that output into `less`, so 
we can look at it more carefully.

```zcat
zcat ERR2020601.fastq.gz | grep "@ERR" | less
```

Remember to press "q" to exit.

And for one final recap, we previously calculated there to be 4720 reads in our 
file. If we have just extracted the unqiue read _headers_ for every read, then 
in principle we can also just count these with `wc`!

```zcat
zcat ERR2020601.fastq.gz | grep "@ERR" | wc -l
```


<p align="center"><img src="https://media.giphy.com/media/11sBLVxNs7v6WA/giphy.gif" width="20%"></p>

## Now you're thinking with portals! Symlinks and their usefulness.

The FASTQ we have been working with so far we downloaded from the ENA. It is 
important to keep the file name intact, so we can easily identify this specific 
FASTQ file in the ENA database in the future, if need be. But talking about 
sample `ERR2020601` is simply not sexy enough, and makes things harder to work 
with, especially when we are working on 15 different and similarly names samples.
We need to come up with a better name for this sample. Something less arbitrary 
and easier to remember. How about `Sample_1`? That sounds much more easily 
identifiable! :neutral_face:

In order to retain the original file but also rename it for convenience we can 
use a _symbolic link (**symlink**)_. You have doubtless seen these many times 
right on your desktop, in the form of desktop shortcuts! They are small portals 
that let you go to a remote location really fast, and take something from there. 
Imagine if you could reach the TV remote from the sofa, although for some strange 
reason you left it in the freezer when picking up the (now half-melted) ice cream. 
_\[No, of course I have never done that!]_

<p align="center"><img src="https://orig00.deviantart.net/784b/f/2014/354/a/3/poor_messing_with_a_portal_gun__gif__by_ritorical-d8ahh8f.gif" width="20%"></p>

So let us make a new subdirectory to store our symlink to the FASTQ file we 
already downloaded, and move to that directory.

```bash
mkdir ~/BareBonesBash/FastQ.Portals
cd ~/BareBonesBash/FastQ.Portals
```
It is now time to make the symlink. We do this with the `ln` command (short for 
"**l**i**n**k"), by providing the `-s` option, which specifies we want to create 
a **s**ymbolic link (i.e. a shortcut).
Tip: You should give absolute paths to the file your symlinks point to, or things 
**will** break down.
```bash
ln -s ~/BareBonesBash/ERR2020601.fastq.gz .
```
Make sure you included that `.` in the command above. As discussed in the "Relative 
Paths" section, that points to the current directory, thus telling the `ln` programme 
that it should create the link in the current directory. You should now see the 
symlink in the directory. To see where the link points to we can use `ls -l`, which
provides exended information on the files shown with `ls`. (For more information you 
can look at the `man` page for `ls`).

```bash
ls -l
```
We can now rename the symlink to give it its sexy new name. You already learned this 
command, so try to work it out, or give either of us a shout. (Hint: It came before 
the bears.)

```bash
for i in {1..15}; do echo -ne "I will not copy paste everything that is in a box mindlessly, but actually read the tutorial.\n"; echo -ne '\007'; done
```

<details>
  <summary> Check here if you need the answer.</summary>
   <p>
     <code>
     mv ERR2020601.fastq.gz Sample_1.fastq.gz
     </code>
   </p>
 </details>
&nbsp; 
We can now look at the original FASTQ file by pointing at our symlink, like so:
```bash
zcat JK2781_MT.fastq.gz | head -n 20 | tail -n 4
```
Which should print out the same read as it did on the original FASTQ file.

## Lazyness 101: Minimising our work by maximising the work of the computer

Now for a bit of honesty. A single sample will not get you a nature publication.
_\[ok, maybe sometimes]._ We will need more data if we're gonna make it to the
most prestigious journals. So let's download another XX samples from James' 
Mammoth project to get us on our way to a nature cover page.

It is a lot of work to run `wget` XX times while changing the command everytime. 
Good thing we're here to learn how to be lazy! We can download multiple files 
from an ftp server by giving `wget` a file that contains the ftp links for each 
file we want downloaded. Copy the text below, and save it as `~/BareBonesBash/
Ftp.Links.txt`, using a text editor of your choice (e.g. `nano`).

<pre>
List of fastQ ftp links
</pre>

And now that we have that file, it is time to actually download the files. You can 
provide a file with ftp links (like the one you just made) using the flag `-i`, for 
"**i**nput". 

```bash
wget -i ~/BareBonesBash/Ftp.Links.txt
```

Look at that! One command instead of 7! You're becoming a bash pro already! Now to 
minimise our workload in making the symlinks! We can do this using a **for loop**, 
one of the basic methods of all programming. 

Imagine you have to order pizzas for a varying number of scientists every week. 
_\[Just a random example]._ For every four people you will need an extra pizza.
This is a sort of "for loop", where you go through the list of names of hungry 
scientists, and you add one more pizza to the list for every four names. For the 
sake of simplicity we will leave the people 

preserve original file, so make symlink in new directory
* mkdir
* ln -s 
* mv (the symlink) ERR2020601.fastq.gz JK2781_MT.fastq.gz
* ls -l (to see)
* download more files from ENA with a provided list.
* small for loop to copy and rename the rest of the fastq.gz with ln -s.
* rev
* cut 
* variables
* for/while loops
* if statements

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
 
