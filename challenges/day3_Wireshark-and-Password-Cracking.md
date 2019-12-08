# Day 3: Wireshark and Password Cracking

## [Challenge 1](#challenge-1-destination-ip-on-packet-number-998) | [Challenge 2](#challenge-2-find-a-password) | [Challenge 3](#challenge-3-what-to-take-to-the-partay)

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