# Day 16: Python and File Scripting

## [Challenge 1](#challenge-1-how-many-files-were-extracted) | [Challenge 2](#challenge-2-decoding-the-cookie-and-finding-the-fixed-value) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

## Challenge 1: How many files were extracted

We're given a zip file that has other zip files. We don't really know how many layers of zip files there are. So, I think a good method would be extracting the files and then keep extracting if any files are zip files, and removing the old zip files so they don't get in the way.

```Python
import zipfile
import os

# the directory that ONLY contains "final-final-compressed.zip"
# change this to the path of your directory
directory = "/home/roost/Desktop/day16/challenge_files"

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
