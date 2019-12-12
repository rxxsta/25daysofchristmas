# Day 7: nmap

## [Challenge 1](#challenge-1-how-many-tcp-ports-open-under-1000) | [Challenge 2](#challenge-2-what-is-the-name-of-the-operating-system-of-the-host) | [Challenge 3](#challenge-3-what-version-of-ssh-is-running) [Challenge 4](#challenge-4-finding-mcinventorys-christmas-request)

This one asks us to do some reconnaissance on our deployed machine. We can get most of our answers with the `nmap`.

## Challenge 1: How many TCP ports open under 1000

We can run `sudo nmap -sT -p 0-1000 <machine-ip>`\
-sT specifies TCP connection
-p specifies ports

This gets us open TCP ports under 1000

## Challenge 2: What is the name of the operating system of the host

We can run `sudo nmap -O <machine-ip>`\
-O tries to determine the operating system running on the specified ip

We can find our answer under "TCP/IP fingerprint"

## Challenge 3: What version of SSH is running

We can run `sudo nmap -sV -p 22 <machine-ip>`\
-sV tries to the determine the version of the services running on open ports\
We use specify port 22 here, because according to our first open port scan, that's what port SSH was running on.

