# Day 1: Encryption

## [Challenge 1](#challenge-1-md5-hashsum-of-note1.txt.gpg) | [Challenge 2](#challenge-2-where-was-elf-bob-told-to-meet-alice) | [Challenge 3](#challenge-3-finding-mcinventorys-christmas-request)

We're given a zip file.\
You can unzip it with `unzip tosend.zip`\
And we get 3 files.\
![zip](https://i.imgur.com/z0Lk1uE.png)

## Challenge 1: md5 hashsum of note1.txt.gpg

The command `md5sum note1.txt.gpg` will give you it's hash.

## Challenge 2: Where was elf Bob told to meet Alice

I have no idea how someone would guess the password for the gpg key.\
Although, it seems kind of easy, I guess.\
The passphrase for note1.txt.gpg is "25daysofchristmas"

Run `gpg -d note1.txt.gpg` and type in the passphrase on prompt.
