# Learning Some Metasploit

## [Challenge 1](#challenge-1-compromise-the-web-server-using-metasploit-and-find-flag1) | [Challenge 2](#challenge-2-what-is-santas-ssh-password) | [Challenge 3](#challenge-3-line-148-on-the-naughty-list) | [Challenge 4](#challenge-4-line-52-on-the-nice-list)

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

~~This meterpreter session has a very limited amount of commands, such as we can't use the find command to look for anything :/ (The `help` command gives you a list of commands that you can run)~~ UPDATE: You can use the `shell` command to switch from the meterpreter shell to a linux shell.

I looked inside the directories that were last modified around the time this challenge was released.\
![last mod](https://i.imgur.com/0o5JJdw.png)

After some digging in these directories I found flag1!
![flag1](https://i.imgur.com/o4FhAk2.png)

## Challenge 2: What is Santa's SSH password

\* *Still inside the web server* *  
Let's go to "/", the main system directory.\
There's a directory called "flag-dir" but with nothing in it...\

After some digging using the same formula as the last challenge. I found Santa's SSH passowrd.\
![santa ssh](https://i.imgur.com/d2Py5ST.png)

## Challenge 3: Line 148 on the naughty list

You can close metasploit.

Now that we have Santa's ssh credentials we can log into his server.\
`ssh santa@<machine-ip>`

Quality shell art!\
![reindeer](https://i.imgur.com/1wSOaMq.png)

There's two list in here.\
![lists](https://i.imgur.com/E0qtU8t.png)

Run `cat naughty_list.txt | grep -n . | grep 148`\
This will filter out for the 148th line.\
`-n` in the grep command prepends each line with its corresponding line number.

## Challenge 4: Line 52 on the nice list

We can run the same command as the last challenge.\
Replace "naughty_list.txt" with "nice_list.txt"\
Replace 148 with 52\
`cat nice_list.txt | grep -n . | grep 52`
