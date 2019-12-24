# Day 20: Cronjob Privilege Escalation

## [Challenge 1](#challenge-1-what-port-is-ssh-running-on) | [Challenge 2](#challenge-2-crack-sams-password-and-read-flag1.txt) | [Challenge 3](#challenge-3-escalate-priviledges-by-taking-advantage-of-a-cronjob-and-reading-flag2)

## Challenge 1: What port is SSH running on

Enumerate with nmap, and we get a service called tram. I *think* it's another service that uses tcp. Apparently, you can use ssh to connect to it!\
![tram](https://i.imgur.com/QsFhVV9.png)

## Challenge 2: Crack sam's password and read flag1.txt

We can use `hydra` and rockyou.txt to try an crack the login credentials.

`hydra -l sam -P /usr/share/wordlists/rockyou.txt <your-ip-address> -t 4 ssh -s <port-ssh-was-found-on>`

And eventually you will get Sam's ssh password!\
![pass](https://i.imgur.com/NRkJkco.png)

And now we can login as him.

The first flag is in Sam's home directory.

## Challenge 3: Escalate priviledges by taking advantage of a cronjob and reading flag2

Once we log in, we should try finding flag2.

![flag2](https://i.imgur.com/ft0ft4P.png)\
It's owned by "ubuntu".

We don't have permission to read it :(\
![perm](https://i.imgur.com/1FNOACh.png)

Let's see what else is ran as ubuntu.\
![clean_up](https://i.imgur.com/BeOMmOH.png)\
The clean_up.sh looks kinda interesting.

We have permissions to read and write in it!\
![nice](https://i.imgur.com/PA68nWh.png)

Let's see what the script does.\
![work](https://i.imgur.com/rVvSZM9.png)

We can test to see if this script is run at all.

I'm going to make a file in the "/tmp/" directory called "lol.txt" and see if get cleaned up.\
![test](https://i.imgur.com/U8kSOVJ.png)

It did get cleaned! So, we know it works, and we have permission to change the script.\
![worked](https://i.imgur.com/tHpFkGC.png)

So, we can give the script the command to put the contents of flag2.txt in a readable location.\
![location](https://i.imgur.com/VKKJQ35.png)

It worked!!\
![flag2](https://i.imgur.com/sYF9kSU.png)
