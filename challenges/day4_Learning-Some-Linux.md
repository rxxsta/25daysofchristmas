# Day 4: Learning Some Linux

## [Challenge 1](#challenge-1-visible-files-in-home) | [Challenge 2](#challenge-2-content-of-file5) | [Challenge 3](#challenge-3-what-file-contains-the-string-password)

After deploying our machine and waiting a while
we have to SSH into this our machine.

The details on how to SSH into our machine is given.
![ssh details](https://i.imgur.com/KLFvgH1.png)

The [man](https://linux.die.net/man/) (manual) pages and `--help` command can be really useful here.

## Challenge 1: Visible files in home

When we log in, we should be in our home directory.
We can check by running `pwd`.
It looks like this is the right directory.

The `ls` lists the contents of the directory we're in.

## Challenge 2: Content of file5

We can use the `cat` command to concatinate file5 and an emptyfile to just print out the content of file5.

![file5](https://i.imgur.com/rdKgxx3.png)

## Challenge 3: What file contains the string password

We can use the `grep` command to search for a pattern inside files.

Looking in the man page we see that the `-r` switch can recursively look inside files for the pattern "password"

![pass](https://i.imgur.com/NyvHjts.png)
The "." (dot) means *this* directory. So, it will like inside all of the files.
