# Build-Serverless-App
Build a Serverless Application using AWS Serverless Services

## Introduction:
This project demonstrates how serverless services are tied together to fulfill the business requirement by providing Secure, scalable and cost optimized solution. Here, User enters fills the forms from User Interface which is deployed as static website in S3 and then it calls the API gateway to reach the correct API endpoint. The backend is running in Lambda and productVisitSendDatatoQueue post the messages to the Simple Message Queue(SQS).From SQS, productVisitHandler Lambda function polls the messages from the queue using Lambda trigger configured at SQS and it puts the message into Dynamo DB(DDB). ProductVisitDataLakehandler Polls the messages from the DynamoDB streams and insert the data into s3.whenever, any modification happens at S3 Bucket such as policy updating or anything cloudtrail monitors all the API calls at the management level and it will informs to the eventbus and the event will be posted to the Simple Notification Service (SNS). From SNS, as part of subscription, Email will be triggered to the emailid which is configured as the SNS subscriber.

## Architecture:

![Image-Serverless](https://github.com/user-attachments/assets/833c3057-ad78-461e-9364-801f8b671cc9)
