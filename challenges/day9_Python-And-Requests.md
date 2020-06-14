# Day 9: Python and Requests

In this challenege, you have to know some programming. Or, at least, it would be a lot easier if you already knopw some programming.

We are given a website to go visit. On this website,it gives us a value of part of the flag and the name of the next page for the next character of the flag.

Here is what the content of the first page looks like (under "/")\
![content](https://i.imgur.com/o2qmnwf.png)

The concatination of the spot next to "value" with each subsequent value is the flag. The stream ends when both value and next page equal to "end".

I don't think you can simply go to all of the pages, there might be way too many! It is a better job for a computer.

## Challenge 1: What is the value of the flag

Here are some links that helped me while writing this script:\
<https://www.datacamp.com/community/tutorials/making-http-requests-in-python>\
<https://www.geeksforgeeks.org/python-string-split/>\
<https://www.geeksforgeeks.org/print-without-newline-python/>

And here is the script I wrote to print out a copy and pastable flag.

```python
import requests

url = "http://10.10.241.214:3000/"
flag = [] # list to hold the flag

# site_content will be in the format as below
# {"value":"<char>","next":"<next page name>"}

site_content = requests.get(url).text

# parses between every "
parsed_content = str.split(site_content,"\"")

# content of 1st page (under "/")
value = parsed_content[3]
next_page = parsed_content[7]
flag.append(value)

while (value != "end" and next_page != "end"):
    urltogoto = url + next_page
    site_content = requests.get(urltogoto).text
    parsed_content = str.split(site_content,"\"")

    value = parsed_content[3]
    next_page = parsed_content[7]

    if value != "end":
        flag.append(value)

# prints flag in a single line for easy copy and paste
for character in flag:
    print(character, end = "")
print() # put the prompt on a new line
```
