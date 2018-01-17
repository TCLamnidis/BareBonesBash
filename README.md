# BareBonesBash
A basic Bash tutorial by @jfy133 and @TCLamnidis.

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

## Introduction

The aim of this tutorial is to make you familiar with using bash everyday... 
for the rest of your life. More specifically, we want to do this in the context
of our work. We will start with how to navigate (Theseus' words...) around a 
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
a directory path and ends with a dollar symbol.

```bash
<username>@<device_name>:~$
```

Here, the directory `~`, stands for your home directory. This shorthand can be 
seen and used both on your machine and on the cluster. Note that this shorthand 
will point to a different place, depending on the machine and the user.

* pwd
* cd (../)
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
