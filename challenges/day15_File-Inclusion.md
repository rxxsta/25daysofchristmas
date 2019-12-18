# Day 1: File Inclusion

## [Challenge 1](#challenge-1-where-is-charlie-booking-a-holiday-to) | [Challenge 2](#challenge-2-read-/etc/shadow/-and-crack-charlies-password) | [Challenge 3](#challenge-3-reading-flag1.txt)

We're given a machine.\
I think it's a good idea, from now on, to first enumerate the ip address we're given and check for open ports/services.

It looks like there is a web server and ssh port open.\
We don't have the credentials to access the ssh server, but the web server we can probably view.\
![enumerate](https://i.imgur.com/wlvO9dk.png)

Here is the website
![site](https://i.imgur.com/IYX0eN9.png)\
Someone uses a website for a note book.

## Challenge 1: Where is Charlie booking a holiday to

Well Charlie has a some notes and a to-do list, you can find it there.\
![holiday](https://i.imgur.com/SCPRRVX.png)

## Challenge 2: Read /etc/shadow and crack Charlie's password

How are the notes being retrieved?

If you look at the source code, there seems to be a custom script.\
![script](https://i.imgur.com/no1yc4O.png)\
It looks like it's getting the notes from `/views/notes/<notename>`.\
And then it has a prepend of `/get-file/`.

We kind of have access `/get-file/`\
But I think they gave us too much access

We can do something called [directory traversal](https://www.acunetix.com/websitesecurity/directory-traversal/) to reach `/etc/shadow/`.

Since `/get-file/` is a directory deeper than where we would like to be at (root directory, "/").\
We have to specify our own path with `/../etc/shadow`.\
The ".." means "one directory level up"

So, our request should look like `http://10.10.106.40/get-file//../etc/shadow`\
But, we have to URL encode part of the path.\
Our final request will end up being `http://10.10.106.40/get-file/%2f..%2Fetc%2Fshadow`.

Which get's us our shadow file and Charlie's hash that we need to crack\
![shadow](https://i.imgur.com/gTVjVF4.png)

### Cracking Charlie's hash

We can use some hashcat and a dictionary to crack the hash.

Copy and paste the hash portion (the red underlined part) into a new file. 
![shadowfile](https://i.imgur.com/gTVjVF4.png)

The hash algorithm it's using is sha512 because of the specified $6$\
The salt is "oHymLspP" because that is the next thing enclosed by $'s
The rest is the password.

Now let's run it with hashcat with the command\
`hashcat -m 1800 <your-file-name> /usr/share/wordlists/rockyou.txt --force`

And you'll get the cracked password :D

## Challenge 3: Reading flag1.txt

We found an ssh service running earlier!\
And now we probably have the credentials to log into it.

Run `ssh charlie@<machine-ip>` and enter his password.

And here it is.\
![sweet sweet flag](https://i.imgur.com/ZTjAVnI.png)\
Our sweet, sweet, flag.
