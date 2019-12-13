# Day 6: Data Exfiltration

## [Challenge 1](#challenge-1-what-data-was-exfiltrated-via-dns) | [Challenge 2](#challenge-2-what-did-little-jimmy-want-to-be-for-christmas) | [Challenge 3](#challenge-3-what-was-hidden-within-the-file)

Oh baby, another pcap. We should start by opening it up with Wireshark.\
This one isn't that big, only 137 frames.

## Challenge 1: What data was exfiltrated via DNS

Let's start by filtering for only packets where its protocol is dns.\
The supporting material gives us an example where dns can be used to transfer hex encoded data!

Once filtered, you can see where it looks funky. I don't think DNS queries have that much info in them.\
This also looks like the one in the example. So, the big long string is probably hex encoded.
![dns exf](https://i.imgur.com/qpu5a3x.png)

You can right click the row/packet, then copy as printable text so you can paste it into a hex to ascii converter.\
And turns out this is our flag!

## Challenge 2: What did Little Jimmy want to be for Christmas

Let's look through all the packets where the http protocol is being used, because the content of http is insecure and we can view/download it.

After applying the filter, we get some promising info!
![http data](https://i.imgur.com/Dj2T14Q.png)\
And it looks like we also might have found the file for the next challenge!!

In Wireshark we can go to `file -> export objects -> http` and view the stuff we can download. So we might as well save them each and look through them for some info.

The html document only gave us the names of the other files that we should probably look through.

Now, let's try and unzip christmaslists.zip

Anddddd it's locked with a password.

### Cracking the christmaslists.zip file

Guess we should google for a zip file cracker in Kali or another tool we can download.

I found this BAD BOY (apparently also in in the supporting documents)
![bad boy](https://i.imgur.com/HDnamkm.png)\
fcrackzip

Too bad Kali doesn't come with it, but we can download it with the command\
`sudo apt install fcrackzip`

And we just replace "numbers.zip" with "christmaslists.zip". I think we could still use rockyou.txt. I don't think they would give us a super hard password just yet... lol

boom
![cracked zip](https://i.imgur.com/NUAbzkw.png)

AND NOW we can unzip it with the password we found.

And we have Little Jimmy's list.
![list](https://i.imgur.com/msg4j4J.png)
The flavor text is kinda funny 😂.

## Challenge 3: What was hidden within the file

It's probably talking about the jpg file. Let's use steghide (as suggested).\
I don't think Kali comes out of the box with this either :(.\
Download it with `sudo apt install steghide`.

run `steghide extract -sf TrHackMe.jpg` and it extracts a hidden text file!

The answer is in the beginning portion of the text.
