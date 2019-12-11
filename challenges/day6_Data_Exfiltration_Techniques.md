# Day 6: Data Exfiltration

## [Challenge 1](#challenge-1-what-data-was-exfiltrated-via-dns) | [Challenge 2](#challenge-2-decoding-the-cookie-and-finding-the-fixed-value) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

Oh baby, another pcap. We should start by opening it up with Wireshark.\
This one isn't that big, only 137 frames.

## Challenge 1: What data was exfiltrated via DNS

Let's start by filtering for only packets where its protocol is dns.\
The supporting material gives us an example where dns can be used to transfer hex encoded data!

Once filtered, you can see where it looks funky. I don't think DNS queries have that much info in them. This also looks like the one in the example. So, underlined that doesn't look normal is probably hex encoded.
![dns exf](https://i.imgur.com/qpu5a3x.png)

You can right click the row/packet, then copy as printable text so you can paste it into a hex and ascii converter.\
And turns out this is our flag!
