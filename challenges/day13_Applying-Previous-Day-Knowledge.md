# Day 1: Accumalted Challenges

## [Challenge 1](#challenge-1-finding-a-hidden-directory-on-the-web-server) | [Challenge 2](#challenge-2-gaining-initial-access-and-reading-user.txt) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

This day combines what we learned/did from the other days into one day.

First let's see what services are running on our deployed machine.\
![services](https://i.imgur.com/41GPFcz.png)\
Looks like it's at least running a web server and [windows remote desktop](https://www.speedguide.net/port.php?port=3389)

Here is the web server, nothing too important seems to be in the starting directory
![web server](https://i.imgur.com/gcPhMEx.png)

## Challenge 1: Finding a hidden directory on the web server

I'm thinking we should use dirbuster for this one.
![dirb](https://i.imgur.com/iOg4DLs.png)

After maybe a few minutes, we get a hit! Along with other files and directories it found.\
![dir](https://i.imgur.com/fWyLOJy.png)

## Challenge 2: Gaining initial access and read user.txt

Looking deeper into `<directory-name>/index.php` (found with dirbuster), I found wade talking about some if his login info.\
![user](https://i.imgur.com/H4tJ7Pc.png)\
Parzival is either his password or username.

Let's go to the login page from the sidebar.\
Let's try "Wade" as his username and "parzival" as his password.

Andddd we're in\
![hax0r](https://i.imgur.com/Ah5bxVJ.png)

...

After some digging around in the wordpress admin page, there doesn't seem to be anything important here.

So, let's try logging into remote desktop that we found open.

I was searching up some ways to log in to remote desktop, such as `rdesktop`, but I had trouble with that one. I found another program, "FreeRDP" that does the same thing and worked for me.

I found the solution
[here](https://www.linuxquestions.org/questions/linux-networking-3/failed-to-connect-credssp-required-by-server-4175611983/)

run `xfreerdp /u:"Wade" /v:<machine-ip>:<port>`\
I guess I'll be using xfreerdp from now on.

And now we're really in!\
The file was on the desktop. Super cool challenge!\
![remote](https://i.imgur.com/Cd0mZWJ.png)
