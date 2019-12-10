# Day 5: Open Source Intelligence Gathering

## [Challenge 1](#challenge-1-finding-lola's-date-of-birth) | [Challenge 2](#challenge-2-content-of-file5) | [Challenge 3](#challenge-3-what-file-contains-the-string-password) | [Challenge 4](#challenge-4-what-file-contains-an-ip-address) | [Challenge 5](#challenge-5-how-many-users-can-log-in)

Here, we are given a picture of the grinch (probably full of grumpy [metadata](https://en.wikipedia.org/wiki/Metadata)).

Kali comes with some tools to dig into the metadata such as `exiv2`.

## Challenge 1: Finding Lola's date of birth

Using exiv2 we can extract the metadata of the image using `exiv2 ex thegrinch.jpg` and it will extract it into a file called "thegrinch.exv".

If we look out the content of that exv file
![meta](https://i.imgur.com/ihJRvld.png)
We see that there seems to be username here!

### Using Sherlock to find where the username belongs to

Kali doesn't come with this, but, there is a super cool tool called [Sherlock](https://github.com/sherlock-project/sherlock) that's perfect for this.\
It searches usernames throughout a whole bunch of social media platforms.

To use in the command line:

1. `git clone https://github.com/sherlock-project/sherlock.git` (downloads the project)

2. `cd sherlock` (moves into the project folder)

3. `sudo python3 sherlock.py JLolax1` (searches social media for JLolax1)

### finding her social media account

There is a couple of duds, but it looks like Lola has a twitter!

![twitter](https://i.imgur.com/bLLhMTo.png)

She has her birthday in her bio
