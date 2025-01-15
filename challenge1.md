## Challange 1
Buckets of Fun

## Challange Statement
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

## Solution

We can list the files using the following command:
aws s3 ls s3://thebigiamchallenge-storage-9979f4b/files/ 

The above command shows that there are two files in the the source. The files are flag1.txt and logo.png

However, we can see the contents of the flag1.txt file using the following two commands:

aws s3 cp   s3://thebigiamchallenge-storage-9979f4b/files/flag1.txt -
curl https://thebigiamchallenge-storage-9979f4b.s3.amazonaws.com/files/flag1.txt

Both commands shows the the content of the file which is  {wiz:exposed-storage-risky-as-usual} that is the flag of this challangge.

