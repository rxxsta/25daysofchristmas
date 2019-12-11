# Day 2: Brute Forcing Directories

## [Challenge 1](#challenge-1-finding-the-hidden-directory) | [Challenge 2](#challenge-2-find-a-password) | [Challenge 3](#challenge-3-what-to-take-to-the-partay)

After the setup of deploying the machine and waiting a few minutes, we are now ready to access the webpage!

The challenge tells us how to reach it

![website access](https://i.imgur.com/eDBZ9KV.png)

We're greeted by this cold penguin
![penguin](https://i.imgur.com/aWt5pSf.png)

## Challenge 1: Finding the hidden directory

The supporting material helps us out. It shows us how we can use DirBuster and some directory lists. If you're using Kali these things come by default!

Some lists we can use are located under
`/usr/share/dirbuster/wordlists/`

### Running dirbuster

Would could also use the commandline dirbuster tool, but a GUI tool is already given to us.
You can search "dirbuster" in the applications of Kali

We can use a small wordlist I think. No way TryHackMe would make it too long to find.
😅

The red means that field was changed
![dirbuster](https://i.imgur.com/kX7wDZZ.png)
Recursive was turned off because otherwise it would take an uber long time. It would search directories within directories!!

We can checkout the results under one of the results tabs.

After a while of dirbuster doing its thing, we get an interesting looking directory with a response code of 200 and it looks like our flag :)
![secret dir](https://i.imgur.com/IEbk8HG.png)

## Challenge 2: Find a password

If we go to that directory, we can see a similar looking page.
![secret](https://i.imgur.com/MBS8Qig.png)

Hmmm let's look at the source code with our browser's developer tools.

![github](https://i.imgur.com/CUtUuOT.png)
Oh hey! Looks like we find the page design for this website on github under the name:
> arctic digital design

So let's try and search them on github
![arctic](https://i.imgur.com/H2AaBR1.png)
Found it!

Looks like it came with default credentials. Rookie mistake..
![rookie mistake](https://i.imgur.com/bBUmzaB.png)

## Challenge 3: What to take to the partay

With the credentials from the last challenge, let's login with them heheh

A little looking around, and we can see what we should bring to the PARTAY!!
![partay](https://i.imgur.com/MfclTZt.png)
