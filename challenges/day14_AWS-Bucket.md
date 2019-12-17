# Day 14: AWS

## [Challenge 1](#challenge-1-name-of-the-file-found) | [Challenge 2](#challenge-2-what-is-in-the-file)

All we're given is a s3 bucket named "advent-bucket-one".

## Challenge 1: Name of the file found

We can look at the URL, advent-bucket-one.s3.amazonaws.com, and see if the the bucket is public.

Lo and behold\
![pub bucket](https://i.imgur.com/dRJTI16.png)

## Challenge 2: What is in the file

We can either go to `bucketname.region-name.amazonaws.com/file-name` or create an account to download and view the file with [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

Since it's probably useful to have an aws account, I'll make one. And also because I don't know how to get the region name. Although, [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html) is a list of the regions you could try.

Anyways\
We have to download and configure the AWS CLI, Kali doesn't come with it.

1. [Create an account](https://portal.aws.amazon.com/billing/signup#/start). (Requires personal info unfortunately)

2. [Install AWS CLI version 2 on Kali](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux-mac.html).

3. Run `aws2 configure`

4.
    1. Go to [security credentials](https://console.aws.amazon.com/iam/home?#/security_credentials)

    2. Open up Access keys

    3. Create New Access Key

    4. Download Key File (rootkey.csv) and keep SAFE (it's like your password)

5. Open up rootkey.csv

6. Copy and paste the keys into the fields respectively.

You can always create a new pair another time, in case something happens to rootkey.csv.

You can now view what files are in the bucket with `aws2 s3 ls s3://advent-bucket-one`\
Download the file with `aws2 s3 cp s3://advent-bucket-one/<file-name> .`\
And then you can see the contents of the file with `cat <filename>`
