# Day 3: Wireshark and Password Cracking

## [Challenge 1](#challenge-1-destination-ip-on-packet-number-998) | [Challenge 2](#challenge-2-item-on-the-christmas-list) | [Challenge 3](#challenge-3-what-to-take-to-the-partay)

This challenege only comes with an *EVIL* pcap (packet capture) file.\
Lucky for us Kali comes with wireshark to analyze the pcap and hashcat to crack any hashes we find!

## Challenge 1: destination IP on packet number 998

Once we download the pcap, we can find it in our downloads folder and wireshark should open it by default.

This is what it will look like
![pcap](https://i.imgur.com/NiBMEaV.png)
We're going to be looking in the "No." column for the 998th packet/frame, and in the "Destination" column for the destination IP of our evil packet.

Wireshark provides a super neat feature of [filtering](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html) out packets.

We can apply the display filter of`frame.number == 998`
![998](https://i.imgur.com/iBU9Jco.png)
and we can find the destination IP easily

## Challenge 2: item on the christmas list

Now that we have the evil packet and the evil destination. let's see what other evil things are going to there.

Let's apply `ip.dst == <destination ip>` to the display filter
![evil destination](https://i.imgur.com/86lUwnH.png)
We find 4 other files.

Through my own experience I know that if the protocol is "Telnet" we can see the data contents isn't encrypted and we can see inside.

Inside of packet number 2255 we see what was put in the list!
![want](https://i.imgur.com/RF6iFQq.png)