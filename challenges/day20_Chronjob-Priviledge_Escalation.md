# Day 20: Cronjob Privilege Escalation

## [Challenge 1](#challenge-1-what-port-is-ssh-running) | [Challenge 2](#challenge-2-decoding-the-cookie-and-finding-the-fixed-value) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

## Challenge 1: What port is SSH running on

Enumerate with nmap, and we get a service called tram. I *think* it's another service that uses tcp. Apparently, you can use ssh to connect to it!\
![tram](https://i.imgur.com/QsFhVV9.png)

