# Day 16: Python and File Scripting

## [Challenge 1](#challenge-1-how-many-files-were-extracted) | [Challenge 2](#challenge-2-how-many-files-contain-version-1.1-in-their-metadata) | [Challenge 3](#challenge-3-which-file-contains-the-password)

## Challenge 1: How many files were extracted

We're given a zip file that has other zip files. We don't really know how many layers of zip files there are. So, I think a good method would be extracting the files and then keep extracting if any files are zip files, and removing the old zip files so they don't get in the way.

Helpful links I used for this challenge:\
<https://www.geeksforgeeks.org/python-finding-strings-with-given-substring-in-list/>\
<https://thispointer.com/python-how-to-check-if-an-item-exists-in-list-search-by-value-or-condition/>

```Python
import zipfile
import os

# the directory that ONLY contains "final-final-compressed.zip"
# change this to the path of your directory
directory = "<path-to-directoy>"

# actively checks to see if the directory specified contains any zips
while any([file_name for file_name in os.listdir(directory) if '.zip' in file_name]): 
    current_directory_content = os.listdir(directory)

    # extract all and remove the zip file we just extracted from
    for file_name in current_directory_content:
        if '.zip' in file_name:
            with zipfile.ZipFile(directory + "/" + file_name, "r") as zip:
                zip.extractall(directory)
            os.remove(directory + "/" + file_name)

print(os.listdir(directory))
print("------------------------")
print("Total number of extracted files: " + str(len(os.listdir(directory))))
```

## Challenge 2: How many files contain Version: 1.1 in their metadata

My Kali machine, and maybe yours too, doesn't seem to come with `exiftool` or the python module. We need them in order for us to script with it. So, we have to install both.

1. `sudo apt install libimage-exiftool-perl` (install cmdline exiftool)

2. `git clone git://github.com/smarnach/pyexiftool.git`

3. `cd pyexiftool`

4. `python setup.py install`

Now you should be able to use it in your python scripts.\
Here is some documentation for [pyexiftool](https://smarnach.github.io/pyexiftool/)\
We want to read ["XMP:Version"](https://www.adobe.com/products/xmp.html) not the ExifTool Version Number

```Python
import exiftool

files = ["<directory-where-your-extracted-files-are"]
count = 0

with exiftool.ExifTool() as et:
    # extracts the values of the tag field XMP:Version from specified files
    versions = et.get_tag_batch("XMP:Version", files)
    for version_number in versions:
        if version_number == 1.1:
          count += 1
print(count)
```

## Challenge 3: Which file contains the password

If you take a look inside any file. It's all gibberish.\
We should try regexing for a string that says "password" (most likely).\
This can also be done with grep, but the point is to program :)

```Python
import os

directory = "<directory-where-your-extracted-files-are>"

list_of_files = os.listdir(directory)

for file_name in list_of_files:
    with open(directory + "/" + file_name, 'r') as reader:
        content_of_file = reader.read().splitlines() # seperates lines into a list
        for line in content_of_file:
            if "password" in line: # if the line contains the string 'password'
                print(file_name)
                print(line)
```
