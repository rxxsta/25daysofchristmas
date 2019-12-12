# Day 7: nmap

## [Challenge 1](#challenge-1-how-many-tcp-ports-open-under-1000) | [Challenge 2](#challenge-2-decoding-the-cookie-and-finding-the-fixed-value) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request) [Challenge 4](#challenge-4-finding-mcinventorys-christmas-request)

This one asks us to do some reconnaissance on our deployed machine. We can get most of our answers with the `nmap`.

## Challenge 1: How many TCP ports open under 1000

We can run `sudo nmap -sT -p 0-1000 <machine-ip>`\
-sT specifies TCP connection
-p specifies ports

This gets us open TCP ports under 1000
