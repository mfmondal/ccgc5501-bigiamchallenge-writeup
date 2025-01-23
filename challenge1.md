# copy the contents of sample.md to start
# Challenge number : 1
Buckets of Fun

## Challenge Statement
We all know that public buckets are risky. But can you find the flag? 

## IAM Policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                }
            }
        }
    ]
}
### write a short analysis about the IAM policy here
From the above policy, from the first json object we can see that any body can get object from s3 bucket named thebigiamchallenge-storage-9979f4b. Similarly according to the second json object any body can list the files from the bucket with the condition that the objects are in the files folder i.e. thebigiamchallenge-storage-9979f4b/files. 

* What do I have access to?
	Any user has access to s3:GetObject and s3:ListBucket in S3 bucket under files folder.
* What don't I have access to?
	No access except get and list object
* What do I find interesting?
	Any body can get and see the objects from files folder in S3 bucket
* etc. i.e. open to public for getting and listing objects


## Solution

We can list the files using the following command: aws s3 ls s3://thebigiamchallenge-storage-9979f4b/files/

The above command shows that there are two files in the source. The files are flag1.txt and logo.png 

However, we can see the contents of the flag1.txt file using the following two commands: 
aws s3 cp s3://thebigiamchallenge-storage-9979f4b/files/flag1.txt 

curl https://thebigiamchallenge-storage-9979f4b.s3.amazonaws.com/files/flag1.txt 

Both commands shows the content of the file which is {wiz:exposed-storage-risky-as-usual} that is the flag of this challenge.


## Reflection
* What was your approach?
	Check the contents in the bucket using aws s3 ls s3://thebigiamchallenge-storage-9979f4b/files/
* What was the biggest challenge?
   	As it was the first challenge, so it was difficult to approach the challenge
* How did you overcome the challenges?
	Just using trial and error method 
* What led to the break through?
	Checking with the Contents of the flag1.txt file
* On the blue side, how can the learning be used to properly defend the important assets? 
	Learning should focus on identifying the assets, security controls and best practices etc.
