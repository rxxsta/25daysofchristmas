# Day 8: Linux Privilege Escalation

## [Challenge 1](#challenge-1-what-port-is-ssh-running-on) | [Challenge 2](#challenge-2-find-and-run-a-file-as-igor-and-read-the-file-home/igor/flag1.txt) | [Challenge 3](#challenge-3-find-another-file-to-run-so-we-can-read-/root/flag2.txt)

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

## Challenge 2: Find and run a file as igor, and read the file /home/igor/flag1.txt

Now that we have the port SSH is hosted on, let's connect to it with Holly's credentials.

`ssh holly@<machine-ip> -p <port-number>`

let's find what programs we can run as igor with:\
`find / -user igor -perm -4000 -exec ls -ldb {} \; 2>/dev/null`

The `find` command is run as igor!
![igor](https://i.imgur.com/EGBWFHj.png)

That means we can use the `-exec` flag with find and output the contents of the flag.\
`find /home/igor/ -name flag1.txt -exec cat {} \; 2>/dev/null`

## Challenge 3: Find another file to run so we can read /root/flag2.txt

So lets see what files have the SUID bit on that run as root.\
We can do that with:\
`find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null | grep -v "/snap"`

"system-control" was changed around the time this day was release\
![root](https://i.imgur.com/vKZi2wf.png)\
let's run that and see what happens

![oo](https://i.imgur.com/TNoEnQz.png)\
It asks for a command and that command is run as root!!

So, we can print the files out of our flag :D\
![flag2](https://i.imgur.com/J1jjKdU.png)
