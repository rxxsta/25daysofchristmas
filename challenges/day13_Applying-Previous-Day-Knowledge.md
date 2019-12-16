# Day 1: Accumalted Challenges

## [Challenge 1](#challenge-1-finding-a-hidden-directory-on-the-web-server) | [Challenge 2](#challenge-2-decoding-the-cookie-and-finding-the-fixed-value) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

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
