# Learning Some Metasploit

## [Challenge 1](#challenge-1-compromise-the-web-server-using-metasploit-and-find-flag1) | [Challenge 2](#challenge-2-what-is-the-name-of-the-operating-system-of-the-host) | [Challenge 3](#challenge-3-what-version-of-ssh-is-running) | [Challenge 4](#challenge-4-name-of-the-file-that-is-accessible-on-the-server-we-found-running)

There's a web server running on the deployed machine.\
We gotta hack into it.
![naughty and nice](https://i.imgur.com/3QrByD7.png)
We're probably going to have to use Metasploit..\
Luckily, Kali comes with Metasploit!

## Challenge 1: Compromise the web server using Metasploit and find flag1

Let's use nmap to see what type of OS the server is running and some open ports.\
![O](https://i.imgur.com/bf5jJLX.png)\
It's running on 32 bit Linux.\
And has ssh, rpcbind, and http running.\

Let's find out what the versions of those services are.
![ver](https://i.imgur.com/YyBWs5j.png)\
The supporting material says that the web server is struts2, but here it says Apache Tomcat. Maybe they're the same thing or similar..

So now let's open up metasploit and try to exploit it and run our own payload.\
`msfconsole`

The supporting material had an almost exact example on what we should do. We can just replace RHOSTS and LHOST.
![sup](https://blog.tryhackme.com/content/images/2019/12/Screenshot-from-2019-12-09-21-07-23.png)

[This](https://www.rapid7.com/db/modules/exploit/multi/http/struts2_content_type_ognl) site says how it is vulnerable.

I had trouble using metasploit on the Kali virtual machine, so I'm using my own personal machine for this day instead.

After running the exploit and payload.\
We are now inside the web server!
![inside](https://i.imgur.com/gqiXrqF.png)\
Now we just hav to find flag1.

This meterpreter session has a very limited amount of commands, such as we can't use the find command to look for anything :/ (The `help` command gives you a list of commands that you can run)

I looked inside the directories that were last modified around the time this challenge was released.\
![last mod](https://i.imgur.com/0o5JJdw.png)

After some digging in these directories I found flag1!
![flag1](https://i.imgur.com/o4FhAk2.png)
