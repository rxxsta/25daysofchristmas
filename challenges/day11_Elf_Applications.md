# Day 11: ELF Applications Challenge

## [Challenge 1](#challenge-1-finding-the-password-inside-creds.txt) | [Challenge 2](#challenge-2-finding-the-filename-running-on-port-21) | [Challenge 3](#challenge-3-finding-the-password-after-looking-through-the-database)

The challenge tells us we should start by scanning the IP.
We can scan for open ports using `nmap`!

`sudo nmap -sS -p- <IP>`
- `sudo` is required here because we are manipulating the connection (only sending one TCP SYN flag)
- `-sS` is for SYN scanning, where nmap just sends a single TCP SYN flag to check if a port is open depending on the port's response
- `-p-` means to scan ALL the ports of the IP
- `-v` is for verbosity

With our scan done we some ports open:

![ports](https://i.imgur.com/HZSdhcg.png)

A few ports stick out to me.

Port 21 - ftp port, which is promising because we might be able to login anonymously 
Port 22 - ssh port, I don't think we can do anything here right now because SSH requires some authentication
Port 2409 - nfs port, which is a "Network File System" which can host files!!
Port 3306 - mysql - looks like we found a mysql database

## Challenge 1: Finding the password inside creds.txt

Because the question is asking to look inside of a file, I think the best place to start would be running `nfs` scripts from nmap.

We can run the following nmap command with nfs scritps to get some more information out of this IP address:

```
sudo nmap --script=nfs* <IP>
```

And looks like it found creds.txt!!

![creds](https://i.imgur.com/RXj8EZA.png)

Apparently, the port 111 (rpcbind) is related to nfs.

We can mount to the network file system like this:

```
sudo mount -t nfs <IP>:/opt/files/ <MOUNT DIRECTORY>
```

Once we mount it to a place in on our machine, we can see the creds.txt file

![file](https://i.imgur.com/80cpOP1.png)

The creds.txt file contains a password! Probably for one of the other challenges.

## Challenge 2: Finding the filename running on port 21

Now for this challenge, it's asking us to connect to the ftp port 21.

We can connect to the port with the following command:

`ftp <IP>`

Using the `anonymous` username and any password.

Once connected we should be able to type `ls` to list the files, but unfortunately this part of the challenge did not work for me so I will have to skip it.


## Challenge 3: Finding the password after looking through the database