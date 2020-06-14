# Day 19: Command Injection

## [Challenge 1](#challenge-1-contents-of-user.txt)

There's not much on the website this time.\
![site](https://i.imgur.com/uzUa6hh.png)\
But apparently McSkidy found an interesting endpoint `/api/cmd`

## Challenge 1: Contents of user.txt

I found another interesting directory that seems to be working, but looks like another command is being ran?\
![cmnd](https://i.imgur.com/IHUBnXU.png)

Let's try ending the previous command with `;` character.\
![pwd](https://i.imgur.com/noaYkDS.png)\
It worked!! We're in the root directory.\
`;` ends the statement so we can start a new command 

We can try putting in a reverse shell or just look for user.txt.

We can look for user.txt with the find command.\
![found](https://i.imgur.com/sKDT3EN.png)\
Found it!

Now we can just use `cat` to print it out.\
![cat](https://i.imgur.com/KEYN11Z.png)
