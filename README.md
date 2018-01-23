# (Bespoke)BareBonesBash(BroughtByBioinformaticians)
A basic Bash tutorial by @jfy133 and @TCLamnidis.
<p align="center"><img src="https://media.giphy.com/media/v58q1se3dZvag/giphy.gif" width="40%"></p>

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><p align="center"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

## Introduction

The aim of this tutorial is to make you familiar with using bash everyday... 
for the rest of your life :smiling_imp::trollface:. More specifically, we want to do this in the context
of our work. We will start with how to navigate _\[Thiseas' words...]_ around a 
filesystem in the terminal, download sequencing files, and then to 
manipulate these. Within these sections we will also show you simple tips and 
tricks to make your life generally easier. In fact, some of these commands we 
only just learnt last week _\[Thanks Aida!]_ and we've been using the terminal 
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
_\[look at Thiseas' magical prompt as an example. James keeps his vanilla as he 
is a barbarian]_.

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
pwd
```

There are two types of filepaths: 
* An **absolute** path will start with the deepest directory in the machine, 
  shown as a `/`. That is the directory path you see in the output of the `pwd` 
  command you just ran.
* Alternatively a **relative** path always begins from your working directory (i.e.
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


Now let's look around at out current location and see what we can find within 
our home directories. We can use the command `ls`, shorthand for "list", which 
will (surprise surprise) list the directory contents.

```bash
ls
```

Your home directory should come equipped with multiple subdirectories like 
"Documents", "Pictures", etc. 

It is now time to start moving _\[navigating]_ towards "the Brandenburger Tor" 
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
absolute path we printed using `pwd` in the previous step. Type `cd`, but don't 
press enter yet! 

<p align="center"><img src="https://media.giphy.com/media/23BST5FQOc8k8/source.gif" width="20%"></p>

Copy and paste the output of the previous `pwd` command 
(which you can see in your terminal does not have the command prompt), after 
the `cd`, then press enter.

For example:

```bash
cd /home/fellows/Documents
```

**BONUS TIP TIME!** Now for one last move, here is a lesser-known trick. When 
using `cd` you can use a dash (`-`) to indicate 'my previous location'. This is 
useful since you can move multiple directories with one `cd` command. So, now, 
to return to our home directory from the documents directory we can type:

```bash
cd -
## And to see our new location <- btw, this is called a comment. 
## In bash they always begin with a '#', but the character differs per programming language
## A commented out line is a line that will not by read by the computer.
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
still work the same :wink:. You can double check both of these by typing `pwd`.

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

<p align="center"><img src="https://media.giphy.com/media/ieGdB2g5kDIkg/giphy.gif" width="20%"> <img src="https://media.tenor.co/images/d82c7edc4b04227b4c973f24b904695f/raw" width="26%"></p>

But don't lose hope, because we can rename things with the `mv` command, 
shorthand for "**m**o**v**e". 

In fact move, as the name suggests, will move a file/folder into a new location, 
also renaming it in the process if necessary. It works by typing `mv`, the old 
location and a target location.

```bash
mv ~/BareBonesBosh ~/BearBonesBash
```

The command above will now move the directory into the same location, but with
as the target location is spelt differently, the directory will now have a 
different name, essentially renaming it to `BearBonesBash`. 

But oh no! Not again! This is not a bash tutorial for ancient bear genomics! 

<p align="center"><img src="https://media.giphy.com/media/IQ9KefLJHfJPq/giphy.gif" width="20%"></p>

Let's just delete that empty directory and start over, using the `rmdir` 
command, short for "**r**e**m**ove **dir**ectory".

```bash
rmdir ~/BearBonesBash
ls ~
```

And now we can create our directory, properly named this time, and change 
directory into it.

```bash
mkdir ~/BareBonesBash
cd ~/BareBonesBash
```

## Playing with files, one bit at a time

So we have places to organise our files... buuut we don't have any files yet! 
Lets change that.

We ain't playing with bears today - that's dangerous (as we saw above), instead
lets play with some Mammoths!

<p align="center"><img src="https://media.giphy.com/media/kbuQOkATEo6VW/giphy.gif" width="20%"> <img src="https://media.giphy.com/media/3o6Zte5Q11lxAu8Q5q/giphy.gif" width="20%"></p>

We're going to use `wget` to download a FASTQ file from the ENA. So while in 
our `BareBonesBash` directory, we will give `wget` the link to the file, and 
we should see a loading bar. Once downloaded (it should be pretty quick),
we can use `ls` to check the contents.

<p align="center"><img src="https://media.giphy.com/media/lAIbbDbcXSZSU/giphy.gif" width="20%"></p>

```bash
wget ftp.sra.ebi.ac.uk/vol1/fastq/ERR202/001/ERR2020601/ERR2020601.fastq.gz
## Then to check if the file is now in our working directory
ls
```

Great! But maybe we want to check we downloaded the right thing. In bash,
with text files you can normally use `cat`, which is used to print the 
contents of a file to the screen. Lets try this with our newly downloaded file.

**BONUS TIP TIME!** If you're anything like Thiseas, who gets triggered at slow 
computer things, and prefer to have the computer do the work for you - try 
typing a couple of characters then press the "TAB" key on your keyboard.

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

**BONUS TIP TIME!** try pressing `ctrl+l`, which will clear your terminal of 
all the junk that was printed to your screen. This does NOT delete those lines, 
it simply scrolls down for you. You can still find all your previous work if
you scroll up.

Now it's time for the inevitable tangent when your tutor thinks of a very 
(un)funny metaphor to explain something!

## Asking the computer for help (it loves helping people)
As we just learned, the FASTQ file we've been playing with is compressed, 
_Zipped_, if you will. We constantly compress files in multiple different ways 
(bams are another example of a compressed file), but **why?** As the name
 suggests, compression saves disk space, so we can have more files stored on 
 our system. 

An everyday example of the benefits of compression comes from music. To keep the 
calculations smaller we'll take a time machine back to 2001 when having one of 
these things made you instantly popular and better geared than James Bond _\[tech-savvy 
Pierce Brosnan, not the trigger-happy Daniel Craig]_:

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

This will open the manual page for `zcat` in a separate screen, which you can 
exit by pressing "q". You can scroll up or down with the arrow keys. At the top 
of the screen you will see the command the manual is for, in this case it 
should read `gzip`. That is because `zcat` is part of the programme `gzip`. You 
will see a long description of the programme, followed by (scroll down) a 
section with all the options available. 

Isn't this great! The option `-l` lists the size of a file in both compressed 
and uncompressed form, as well as the compression ratio (how effective the 
compression was). **Most programmes you will use DO have a `man` page, making 
this command extremely useful.**. Now that we learned about the `-l` option of 
`gzip`, let's use it to see how efficient the compression of this FASTQ file is. 
_**\[Say it with us: "`man` is love. `man` is life."]**_


```bash
gzip -l ERR2020601.fastq.gz
```

A compression factor of `74.9%` is pretty good. It means our compressed FASTQ file is 
25.1% the size of the uncompressed file would.

## The Lord of the Pipes: One command to do them all.

After that tangent, let's get back to our regularly scheduled program(ming)!

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

The same option exists for tail, note that but options are not universal! Not 
every programme will use the same options!

```bash
zcat ERR2020601.fastq.gz | tail -n 4
```

And you can also chain them altogether _\[not unlike a human centipede... No 
gif here so I don't get fired]_

```bash
zcat ERR2020601.fastq.gz | head -n 20 | tail -n 4
```

The above command will print the whole file, but capture only the first 20 
lines, before printing out the last 4 lines of these 20.

<p align="center"><img src=".gifs/frodo.gif" width="30%" height="20%"></p>

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
standard question would be, **how many reads are in this FASTQ file?** We know 
now that each read record in a FASTQ file has four components, and takes up 4 
lines. So if we count the number of lines in a file, then divide by four, we 
can work out how many reads are in our file. 

<p align="center"><img src="https://media.giphy.com/media/l41YtZOb9EUABnuqA/giphy.gif" width="20%"></p>

For this we can use 'wc', which stands for "**w**ord **c**ount". However, we 
don't want to count words, we want to count the number of lines. We can 
therefore use the flag `-l` to do this (try using what we learnt above to 
find lists of these flags!). But remember we first have to decompress the lines 
we are reading from the file with `zcat`.

```bash
zcat ERR2020601.fastq.gz | wc -l
```

This should give us 18880, which divided by four (since there are four lines 
per read), is 4720 reads.

Finally, maybe we want to know what the name of each read is. When we used
less above, we saw each read header began with "@". Maybe we can use this
to our advantage!

<p align="center"><img src="https://media.giphy.com/media/3orieUe6ejxSFxYCXe/giphy.gif" width="20%"></p>

The command `grep` will only print lines in a file that match a certain 
pattern. So for example, we want to search for every line in our FASTQ file 
that contains a '@'. Lets try it out again in combination with `zcat` and 
our pipes.

```zcat
zcat ERR2020601.fastq.gz | grep "@"
```

Unfortunately we seem to have picked up some other stuff because of the @ 
characters in the base quality lines. We can make our "pattern", in this 
case `"@"`, more specific by adding "ERR" to it. But let's also avoid flooding 
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
FASTQ file in the ENA database in the future, if need be. 

In order to retain the original file we can use a _symbolic link (**symlink**)_.
You have doubtless seen these many times right on your desktop, in the form of 
desktop shortcuts! They are small portals that let you go to a remote location 
really fast, and take something from there. Imagine if you could reach the TV 
remote from the sofa, although for some strange reason you left it in the freezer 
when picking up the (now half-melted) ice cream. _\[No, of course I have never 
done that!]_

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
Note: You should give _absolute_ paths to the file your symlinks point to, or 
things **will** break down. (Note that a path that starts with `~` is technically 
an absolute path, since it is also not relative to your current position.)

```bash
ln -s ~/BareBonesBash/ERR2020601.fastq.gz .
```

Make sure you included that `.` in the command above. As discussed in the 
"Relative Paths" section, that points your current working directory, thus 
telling the `ln` programme that it should create the link in the current 
directory. You should now see the symlink in the directory. 

<p align="center"><img src="https://78.media.tumblr.com/0ac8df83e4b5ee82c150048347a7db01/tumblr_n1blyfhvTY1qfbz1so1_500.gif" width="30%"></p>

To see where the link points to we can use `ls -l`, which provides exended 
information on the files shown with `ls`. (For more information you can look 
at the `man` page for `ls`).

```bash
ls -l
```

We can now look at the original FASTQ file by pointing at our symlink, like so:
_\[The command looks the same as in the section above, but we are in a different 
directory, so `ERR2020601.fastq.gz` is technically different. It is now a shortcut 
to the originl file, which happens to have the same name.]_

```bash
zcat ERR2020601.fastq.gz | head -n 20 | tail -n 4
```

Which should print out the same read as it did on the original FASTQ file.

## Lazyness 101: Minimising our work by maximising the work of the computer

Now for a bit of honesty. A single sample will not get you a nature publication.
_\[ok, maybe sometimes]._ We will need more data if we're gonna make it to the
most prestigious journals. So let's download another 8 samples from James' 
Mammoth project to get us on our way to a nature cover page.

It is a lot of work to run `wget` 8 times while changing the command everytime.

**Bonus tip time!** One way would be to press the 'up' arrow on your keyboard,
which will allow you to scroll through all your previous commands. Thus you 
could pull up the previous command, then just change a couple of characters.
This can be useful in certain cases, but doing that 8 times is **still** too much 
work.

Good thing we're here to learn how to be lazy! We can download multiple files 
from an ftp server by giving `wget` a file that contains the ftp links for each 
file we want downloaded. Copy the text below, and save it as `~/BareBonesBash/
Ftp.Links.txt`, using a text editor of your choice (e.g. `nano`).

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

**NANO INSTRUCTIONS GO HERE (or before the links?) Also explain the #?**

And now that we have a file with all the ftp links, it is time to actually download 
the files. You can provide a file with ftp links (like the one you just made) using 
the flag `-i`, for "**i**nput". 

```bash
cd ~/BareBonesBash
wget -i ~/BareBonesBash/Ftp.Links.txt
```

Look at that! One command instead of 7! You're becoming a bash pro already! Now to 
minimise our workload in making the symlinks! We can do this using a **for loop**, 
one of the basic methods of all programming. 

Imagine you have to order pizzas for a varying number of scientists every week. 
_\[Just a random example]._ For every person you will need an extra pizza. This 
is a sort of "for loop", where you go through the list of names of hungry 
scientists, and you add one more pizza to the list for every name. Note that the 
specific names of the scientists wouldn't really mattter here, only the number of 
names. So in pseudocode (code-like writing that is human readable but a computer 
will not understand it) the above loop would look like this:

```
for every scientist:
  Order another pizza
done
```

<p align="center"><img src="https://media1.tenor.com/images/5ef4336be26e478431f85b349ec6bd34/tenor.gif?itemid=4149888" width="20%"></p>

Let's stop daydreaming of pizza now and return to the task at hand. For each FASTQ 
file we want to make a symlink to that file. Following the above example, but this 
time putting it into code directly, we get:

```bash
for fastq in ERR2020609.fastq.gz ERR2020611.fastq.gz ERR2020567.fastq.gz ERR2020565.fastq.gz ERR2020613.fastq.gz ERR2020618.fastq.gz ERR2020617.fastq.gz; do 
  ln -s ~/BareBonesBash/$fastq ~/BareBonesBash/FastQ.Portals
done
```

In the above example `fastq` (case-sensitive) is **a variable**. A variable can 
be "set" (i.e. telling the computer what that means) to a variety of things. In 
this case it is set to a **string** of characters, corresponding to the name 
of the first FASTQ file (`ERR2020617.fastq.gz`). At that point the command 
given within the loop (in this case `ln -s`) is executed, before the next FASTQ 
file in the list (`ERR2020611.fastq.gz`) s picked up, and the loop is repeated. 

In other words:

```bash
for every_object in a_list; do
	<this_command> on <this_object>
done
```
Note that you need to separate out your 'loop' from the command itself using
`; do`, and finish the loop with `done`, otherwise bash will keep waiting for
some other input.

Within that command itself, we wish to use what is in the `fastq` variable, 
so we tell the computer we are looking for what is contained in the variable 
by prefixing the character `$` to the variable name. This means that when 
reading `~/BareBonesBash/$fastq`, the computer knows that `$fastq` means 
"use what ever is stored in the variable `fastq`", thus seeing 
`~/BareBonesBash/ERR2020609.fastq.gz`. In the second part of the command 
(`~/BareBonesBash/FastQ.Portals`), there is no `$` in front of the sequence of 
letters `FastQ`, so the computer reads it as the letters themselves and not 
the contents of a variable (which is what we wanted to happen). The word is 
also in different case, so it would **NOT** be read as the variable even with 
the `$` character. See the example below for more info:

```bash
(echo -e "$FastQ <---- Not a set variable"
echo -e "$fastq <---- The last FastQ file in the list of files in the loop.")
```

However, this not the only way to write a loop. In the example above, we 
still have to do a lot of writing, to write out the name of every file. But worry 
not, this is Lazyness 101, and here we like to **NOT** write a lot! It is our 
_right_ not to type more than we need to! It is therefore our right - nay, 
our _responsibility_ - to use **wildcards** "refers to a character that can be 
substituted for zero or more characters in a string". In bash, the wildcard 
character is the asterisk (`*`) _\[Not to be confused with Asterix (Really, 
James? REALLY!?)]_. Therefore, we can use the wildcard to tell bash the loop 
should be performed on ALL items in a directory that match the criterion given. 

If we want to create a symlink (with `ln -s`) for every item within the 
`~/BareBonesBash` directory, and place that symlink within the 
`~/BareBonesBash/FastQ.Portals` directory, we could use: 
```bash
for fastq in ~/BareBonesBash/*; do
	ln -s $fastq ~/BareBonesBash/FastQ.Portals
done

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
for fastq in ~/BareBonesBash/ERR*.gz; do
	gzip -l $fastq
done

```

Therefore, loops allow us to do repetitive tasks, and reap the rewards thereof, 
without having to do all the repetitive work! 
<p align="center"><img src="https://media.giphy.com/media/3rgXByefj5zvCcodOM/giphy.gif" width="40%"></p>

----

## TO DO NOW:

* Table with commands that are in this tutorial before Introduction.
* Introduce echo early on
* Add nano
* Redo Comment description (GIF WITH NINJA!)
* Typo checks
* Swap ( to _\[_ where it's our voices and not part of the tutorial.
* Run through

## DIE ZUKUNFT

* rev
* cut
* find
* awk
* sed
* parallel
* while loops
* if statements
* bash arithmetic "$((8*8))"
* double and single quotes (or in grep and loops)
 
