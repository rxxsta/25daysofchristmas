# Learning Some Metasploit

## [Challenge 1](#challenge-1-how-many-tcp-ports-open-under-1000) | [Challenge 2](#challenge-2-what-is-the-name-of-the-operating-system-of-the-host) | [Challenge 3](#challenge-3-what-version-of-ssh-is-running) | [Challenge 4](#challenge-4-name-of-the-file-that-is-accessible-on-the-server-we-found-running)

There's a web server running on the deployed machine.\
We gotta hack into it.
![naughty and nice](https://i.imgur.com/3QrByD7.png)
We're probably going to have to use Metasploit..\
Luckily, Kali comes with Metasploit!

## Challenge 1: Compromise the web server using Metasploit and find flag1

Let's use nmap to see what type of OS the server is running and some open ports.\
![O](https://i.imgur.com/bf5jJLX.png)\
It's running on 64bit Linux.\
And has ssh, rpcbind, and http running.\
Let's find out what the versions of those services are.\
![ver](https://i.imgur.com/YyBWs5j.png)
