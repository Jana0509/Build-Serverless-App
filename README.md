# Build-Serverless-App
Build a Serverless Application using AWS Serverless Services

--------------------------------------------------------------------
## Introduction:
This project demonstrates how serverless services are tied together to fulfill the business requirement by providing Secure, scalable and cost optimized solution. Here, User enters fills the forms from User Interface which is deployed as static website in S3 and then it calls the API gateway to reach the correct API endpoint. The backend is running in Lambda and productVisitSendDatatoQueue post the messages to the Simple Message Queue(SQS).From SQS, productVisitHandler Lambda function polls the messages from the queue using Lambda trigger configured at SQS and it puts the message into Dynamo DB(DDB). ProductVisitDataLakehandler Polls the messages from the DynamoDB streams and insert the data into s3.whenever, any modification happens at S3 Bucket such as policy updating or anything cloudtrail monitors all the API calls at the management level and it will informs to the eventbus and the event will be posted to the Simple Notification Service (SNS). From SNS, as part of subscription, Email will be triggered to the emailid which is configured as the SNS subscriber.

-----------------------------------------------------------------
## Architecture:

![Serverless Architecture](https://github.com/user-attachments/assets/870be85d-1e71-4551-b374-506cb6d1d032)


-------------------------------------------------------------------
## Project Highlights:

1. S3 Static Website : Leveraged Static Website feature of S3 to deploy the frontend.

2. API Gateway : It is used to create, manage and deploy the APIs, I have created and deployed the REST API which triggeres the Lambda.

3. Lambda : Leveraged the serverless compute Lambda function for running the backend code developed in nodejs.

4. Simple Queue Service : It is used to decouple the producer and consumer. I have utilized this service to post the object payload from ProductVisitSendDataToQueue Lambda.

5. Dynamo DB : Utilized the NO-SQL DB and stored the Json payload object for persistance solution.

6. Dynamo DB streams: Created the DDB stream and it will trigger events if new or modifying happened to the DDB table. In this project, Event will be triggered for the new inmage getting inserted to the DDB.

7. CloudTrail : This service that records and monitors API calls and other actions made to an Amazon Web Services (AWS) account. When any modifying happens at the S3 bucket level, Cloudtrail capture the API activity and report to the EventBridge.

8. EventBridge [CloudWatch Events] : Created the EventBridge rule and triggers it if any event happens at the bucket level via cloudtrail and send its the destination services.

9. Simple Notification Service : It's the Notification Services where Messages will be received in the topic and can be subscribed by multiple destinationm services. Here, we have used email service as the subscriber to trigger the email if any event happens at the bucket level via cloudtrail


----------------------------------------------------------------------
## Key Learning Outcomes:

1. Understand the Synchronous, Asynchronous and Event Based[Poll-Based] Lambda Invocation methods: Lambda triggering from API Gateway is the Synchronous way of invocating the lambda whereas subscribing the event from the SQS Queue is the Async way of invocation. Finally, Event based like dynamodb stream and kinesis, Lambda has to poll from the Event source.

2. Integration Services : Learned how integration services such as SQS, SNS and Dynamo DB events are helping the business requirement to decouple the components and helping to scale independently.

3. Serverless Approach : Learned and utilized the serverless services to create the solution for the Business critical application.

-------------------------------------------------------------------
## Conclusion:
This Serverless application leverages various AWS services to create the business application. From infrastructure design to deployment, this project showcases how application can be powered using Serverless Services.
