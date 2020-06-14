# Day 3: Wireshark and Password Cracking

## [Challenge 1](#challenge-1-destination-ip-on-packet-number-998) | [Challenge 2](#challenge-2-item-on-the-christmas-list) | [Challenge 3](#challenge-3-crack-buddys-password)

This challenege only comes with an *EVIL* pcap (packet capture) file.\
Lucky for us, Kali comes with wireshark to analyze the pcap and hashcat to crack any hashes we find!

## Challenge 1: destination IP on packet number 998

Once we download the pcap, find it with the file explorer and open it. Wireshark should open it by default.

This is what it will look like
![pcap](https://i.imgur.com/NiBMEaV.png)
We're going to be looking in the "No." column for the 998th packet/frame, and in the "Destination" column for the destination IP of our evil packet.

Wireshark provides a super neat feature of [filtering](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html) out packets.

We can apply the display filter of`frame.number == 998`
![998](https://i.imgur.com/iBU9Jco.png)\
and we can find the destination IP easily

## Challenge 2: item on the christmas list

Now that we have the evil packet and the evil destination. Let's see what other evil things are going to there.

Let's apply `ip.dst == <destination ip>` to the display filter
![evil destination](https://i.imgur.com/86lUwnH.png)
We find 4 other files.

Through my own experience I know that if the protocol is "Telnet" we can see the data contents isn't encrypted and we can see inside.

Inside of packet number 2255 we see what was put in the list!
![want](https://i.imgur.com/RF6iFQq.png)

## Challenge 3: Crack buddy's password

### Looking for more info

Inside of packet no. 2906 we see that someone output the contents of the shadow file. \
The shadow file contains the hashed values of passwords of all the users.\
![shadow](https://i.imgur.com/IXGGDCe.png)

We can right click the packet and follow the tcp stream to see what the server replied back.
![follow](https://i.imgur.com/T2M04io.png)

We can see the contents of the shadow file! (because it is still using the Telnet protocol)
![hashes](https://i.imgur.com/Ctg5kzJ.png)

### Buddy's hash

And we found buddies hash
![buddy hash](https://i.imgur.com/hmvtgvg.png)

This part of the hash:\
![sha](https://i.imgur.com/49rzPJN.png)\
tells us that this hash is encrypted with SHA-512.\
Here is some more [info](https://www.cyberciti.biz/faq/understanding-etcshadow-file/) on how this is encrypted.

The supporting documents helps out with showing us what to do with this data.\
It tells us we can use hashcat (popular password cracking tool).

Lets put the hash info into a file\
`echo "$6$3GvJsNPG$ZrSFprHS13divBhlaKg1rYrYLJ7m1xsYRKxlLh0A1sUc/6SUd7UvekBOtSnSyBwk3vCDqBhrgxQpkdsNN6aYP1" > hash`

Before we can run hashcat. Since we are using Kali, there's passwords lists for us like rockyou.txt, but they're gzipped.\
run: `gzip -d /usr/share/wordlists/rockyou.txt.gz` to unzip

### Running hashcat to crack Buddy's password

Now we can run hashcat to try and crack buddy's password.\
`hashcat -m 1800 hash /usr/share/wordlists/rockyou.txt --force`\
`-m` is so you can specify the hash type that you want hashcat to use\
`1800` is the SHA-512 code\
`--force` ignores warnings

After a very short time, hashcat poops out a password for us :)
![pass](https://i.imgur.com/t8vjvaA.png)
