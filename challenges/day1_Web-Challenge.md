# Day 1: Web Challenge

After the setup of deploying the machine and waiting a few minutes, we are now ready to access the webpage!

The challenge tells us how to reach it

![website access](https://i.imgur.com/eDBZ9KV.png)

We're greeted by this cute little elf
and a login screen
![elf](https://i.imgur.com/z4v17ED.gif)

## Challenge 1: Finding the name of the cookie used for authentication

The supporting documentation tells us that using "Burp Suite" is an option. But, for today, we can just use our browser's developer options.

It asks us for the authentication cookie, so that means we can probably register as a user and view what cookis are used once we login.

### Make a user account

![register screen](https://i.imgur.com/n2neaSk.png)

Now we can login with the same credentials

### Find the cookie 🍪🍪

Let's look for some cookies! You can hit `f12` to shorcut to the developer tools. I'm using firefox (default kali browser), so if you're using chrome or another browser it will look slightly different.

For firefox, you can find them under the storage tab
![cookie](https://i.imgur.com/eXCey2g.png)

## Challenge 2: Decoding the cookie and finding the fixed value

In the last challenge we can also see the value of the cookie.
But what the heck is it encoded in? A quick google search and a look in the supporting documentation suggests that it is most likely [Base64](https://stackoverflow.com/questions/201479/what-is-base-64-encoding-used-for) encoded.

### Google for a [base64 to text decoder](https://cryptii.com/pipes/base64-to-text) and decode the cookie value

Copy the value of the cookie, and paste it into the decoder.
You might get an error because the copied cookie value has an appendage of `%3D%3D`. This is [UTF-8](https://www.w3schools.com/tags/ref_urlencode.asp) encoded rather than Base64! So in our decoder we should change `%3D%3D` to `==`.