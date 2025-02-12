## Challenge number : 4

## Challenge Statement:
Admin Only?
We learned from our mistakes from the past. Now our bucket only allows access to one specific admin user. Or does it?

## IAM Policy:

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                },
                "ForAllValues:StringLike": {
                    "aws:PrincipalArn": "arn:aws:iam::133713371337:user/admin"
                }
            }
        }
    ]
}

## Write a short analysis about the IAM policy here:
From first object in the above policy, we can see that any body can download object from s3 bucket named thebigiamchallenge-admin-storage-abf1321. Similarly, according to the second json object with ‘ForAllValues’ condition only admin user can list the files from files folder in the bucket.

## Solution
We can list the files from a specific bucket using the following command: aws s3 ls s3://thebigiamchallenge-admin-storage-abf1321/files/ but without admin user it showed access denied error because only admin user can list the files. However, we can bypass it using the –no-sign-request like the following:
* aws s3 ls s3://thebigiamchallenge-admin-storage-abf1321/files/ --no-sign-request
 
The above command shows that there are two files in the source. The files are flag-as-admin.txt and logo-admin.png

However, we can see the contents of the flag-as-admin.txt file using the following two commands:

* aws s3 cp s3://thebigiamchallenge-admin-storage-abf1321/files/flag-as-admin.txt -
* curl https://s3.amazonaws.com/thebigiamchallenge-admin-storage-abf1321/files/flag-as-admin.txt

Both commands show the content of the file which is {wiz:principal-arn-is-not-what-you-think} that is the flag of this challenge.
 
## Reflection:
* What was your approach?
  Check the contents in the bucket using aws s3 ls s3:// thebigiamchallenge-admin-storage-abf1321/files/
* What was the biggest challenge? 
  To by-pass the admin user to see contents of the files folder in the bucket
* How did you overcome the challenges?
  Using –no-sign-request i.e. aws s3 ls s3://thebigiamchallenge-admin-storage-abf1321/files/ --no-sign-request
* What led to the break through? 
  Checking with the contents of the flag-as-admin.txt file
* On the blue side, how can the learning be used to properly defend the important assets?
  Learning should focus on identifying the assets, security controls and best practices etc.

 
