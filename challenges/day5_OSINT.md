# Day 5: Open Source Intelligence Gathering

## [Challenge 1](#challenge-1-finding-lolas-date-of-birth) | [Challenge 2](#challenge-2-lolas-occupation) | [Challenge 3](#challenge-3-what-phone-does-lola-make) | [Challenge 4](#challenge-4-what-date-did-lola-first-start-photography) | [Challenge 5](#challenge-5-what-famous-woman-does-lola-have-on-her-web-page)

Here, we are given a picture of the grinch (probably full of grumpy [metadata](https://en.wikipedia.org/wiki/Metadata)).

Kali comes with some tools to dig into the metadata such as `exiv2`.

## Challenge 1: Finding Lola's date of birth

Using exiv2 we can extract the metadata of the image using `exiv2 ex thegrinch.jpg` and it will extract it into a file called "thegrinch.exv".

If we look out the content of that exv file
![meta](https://i.imgur.com/ihJRvld.png)\
We see that there seems to be username here!

### Using Sherlock to find where the username belongs to

Kali doesn't come with this, but, there is a super cool tool called [Sherlock](https://github.com/sherlock-project/sherlock) that's perfect for this.\
It searches usernames throughout a whole bunch of social media platforms.

To use in the command line:

1. `git clone https://github.com/sherlock-project/sherlock.git` (downloads the project)

2. `cd sherlock` (moves into the project folder)

3. `chmod +x ./install_packages.sh` (set execute access so we can run the script)

4. `./install_packages.sh` (installs dependencies)

5. `sudo python3 sherlock.py JLolax1` (searches social media for JLolax1)

### Finding her social media account

There is a couple of duds, but it looks like Lola has a twitter!

![twitter](https://i.imgur.com/bLLhMTo.png)

She has her birthday in her bio.

## Challenge 2: Lola's occupation

It's also in her bio.

## Challenge 3: What phone does Lola make

She made a tweet about it.

## Challenge 4: What date did lola first start photography

I didn't know about this one (thank you helpful documents)!\
We can use [Wayback Machine](https://web.archive.org) to give us some snapshots of when her website (her website is in her bio) was changed.

## Challenge 5: What famous woman does Lola have on her web page

The challenege is probably talking about this ~~bad bitch~~ woman
![queen](https://lolajohnson1998.files.wordpress.com/2019/10/reverse_image_search.jpg)\
The file on the website was even called "reverse_image_search.jpg" lol. So, that's what we'll do!

Go to https://images.google.com and click the little camera button and either post the url or upload the image.
