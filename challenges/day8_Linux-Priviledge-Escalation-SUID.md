# Day 8: Linux Privilege Escalation

## [Challenge 1](#challenge-1-what-port-is-ssh-running-on) | [Challenge 2](#challenge-2-decoding-the-cookie-and-finding-the-fixed-value) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

In this day, we are eventually trying to get root privilege.

We are given the login credentials of a user\
![user](https://i.imgur.com/5dDYhhE.png)\
Although, SSH is not on port 22 this time

## Challenge 1: What port is SSH running on

I guess we have to port scan ALL ports because I'm not sure where they would put SSH instead.

Let's run nmap.\
You might want to do something else for a few minutes because it will take a while depending on how fast your computer is.

`nmap -sS -p 0-65535 <machine-ip>`\
-sS is for a TCP stealth that only sends one packet to see if the TCP port is open. Otherwise, I think it would take a lot longer.

We just wanted to see if any ports were open and then go from there. But after this scan we can see there's only one port open.\
This is most likey our SSH port we were looking for.
