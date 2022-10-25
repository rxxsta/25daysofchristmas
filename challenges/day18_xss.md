# Day 18: XSS Challenge

## [Challenge 1](#challenge-1-finding-the-admin-authid-cookie-value)

The challenge mentions that we can access the webpage at: `http://[your-ip-address]:3000`

We're greeted by a login screen, and it looks like we can register a user!

![front](https://i.imgur.com/vfamgkf.png)
## Challenge 1: Finding the Admin authid cookie value

Let's go ahead an register a user and login

![register](https://i.imgur.com/UmxVBS5.png)

There's a nice little box where we can input, this is probably vulnerable to cross-site scripting (description mentioned it).
![entry](https://i.imgur.com/X2tNSMy.png)

We can check if it's vulnerable by injecting the following JavaScript script into the entry box:

`<script>alert(document.cookie);</script>`
`document.cookie` 

retrieves the cookie of our logged in user.

And looks like it's vulnerable because we get an alert box with our cookie!
![alert](https://i.imgur.com/p67wFWQ.png)

But we are really looking for the admin cookie.
If we inject cross-site scripting code into the comments we can hope the admin sees it!

Let's setup a reverse listener premitively for when the admin get hacked.

`nc -lvp 1337`
- `nc` is the `netcat` program to talk across the network
- `-l` is to tell `netcat` we want to listen for connections
- `-v` is for `netcat` to tell us everything that's happening with connections
- `-p` we can specify a port to listen for connections

![nc](https://i.imgur.com/H2fi1hR.png)

And create the malicious cross-site scripting code and send it:

![xss](https://i.imgur.com/UXXTNO2.png)

And we get a hit with our admin authid flag!!
![admin-cookie](https://i.imgur.com/iaWPuci.png)