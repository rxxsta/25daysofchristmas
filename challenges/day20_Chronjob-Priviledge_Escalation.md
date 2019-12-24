# Day 20: Cronjob Privilege Escalation

## [Challenge 1](#challenge-1-what-port-is-ssh-running-on) | [Challenge 2](#challenge-2-crack-sams-password-and-read-flag1.txt) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

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
