# Day 1: Hydra

## [Challenge 1](#challenge-1-using-hydra-to-brute-force-Mollys-web-password) | [Challenge 2](#challenge-2-using-hydra-to-brute-force-Mollys-ssh-password)

Kali comes with Hydra so we don't have to install anything.

Like always, we should see what services are running.\
![nmap](https://i.imgur.com/gKddkd6.png)

Here is the web site we're going to brute force lol.\
![santa bum](https://i.imgur.com/SDevpZY.png)

They tell us that we can use rockyou.txt as the dictionary.

Here is some supporting material to look through:\
<https://blog.tryhackme.com/hydra/>\
<https://en.kali.tools/?p=220>

## Challenge 1: Using Hydra to brute force Molly's web password

THIS WILL TAK A LONG TIME, I THINK 900k-1MIL ATTEMPTS
DO THE SSH CHALLENGE FIRST THEN THIS

You can see what method is being used in the source code.\
![post](https://i.imgur.com/vnoMnH9.png)\
We need to make sure we are using `http-post-form` protocol.

`hydra -l molly -P /usr/share/wordlists/rockyou.txt <ip> http-post-form "/<login url>:username=^USER^&password=^PASS^:F=incorrect" -V`

While this was running in the background and after the SSH challenge, I did some looking around the ssh server with Molly's credentials, and found the answer another way!

In `/home/ubuntu/elf/` is your flag.

## Challenge 2: Using Hydra to brute force Molly's ssh password

This will get you what you're looking for.

`hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.170.16 -t 4 ssh -V`

And when you login with her credentials you will see the flag.
