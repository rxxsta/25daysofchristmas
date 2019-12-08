# Day 1: Web Challenge

## [Challenge 1](#challenge-1-finding-the-name-of-the-cookie-used-for-authentication) | [Challenge 2](#challenge-2-decoding-the-cookie-and-finding-the-fixed-value) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

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
But what the heck is it encoded in? A quick google search and a look in the supporting documentation suggests that it is most likely [base64](https://stackoverflow.com/questions/201479/what-is-base-64-encoding-used-for) encoded.

### Use a [base64 to text decoder](https://cryptii.com/pipes/base64-to-text) and decode the cookie value

Copy the value of the cookie, and paste it into the decoder.
You might get an error because the copied cookie value has an appendage of `%3D%3D`. This is [UTF-8](https://www.w3schools.com/tags/ref_urlencode.asp) encoded rather than Base64! So in our decoder we should change `%3D%3D` to `==`. I'm not too sure why it was like that, maybe put on purpose to trick us a little??

Oh wow! Our username is being used as part of our authentication cookie, that's probably not secure.
![decoded cookie](https://i.imgur.com/1L4IOsO.png)

### Checking to see what part of the cookie is static

One way to test this is registering a new user and looking at it's cookie value. It should be different than the one we just found, right?

So, logout and create a new user and login with it
(I mispelled santa 😬)
![santa user](https://i.imgur.com/13QsBwt.png)

Now doing the same steps we did for the last cookie,
we can see that the part after our username is being used again!!!
![same cookies](https://i.imgur.com/oFf7B9o.png)

## Challenge 3: Finding mcinventory's christmas request

So, we know that out usernames are being used as part of the cookie. So what happens if we make our OWN cookie and try to change that part to "mcinventory".
Let's try it.

### Trying to pretend to be mcinventory by changing our cookie

1. First change the setting of our decoder to encoder. That way we can plug it back in as the same encoding type.

2. Prepend "mcinventory" and the static portion of the cookie (challenge 2).

3. Use the encoding of our new cookie and paste into the same section from where we originally got it

4. Press enter and reload the page so our cookie sets

Holy cow it worked!
![mcinventory](https://i.imgur.com/BYAJD7S.png)

Looks like he was an admin :O

And from here we can see what was on his approval list? Guess he was in charge of approvals and looks like he approved his own gift LOL
