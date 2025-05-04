# AWS Lambda
AWS Lambda lets you run code as functions without provisioning or managing servers.
Lambda-based applications are composed of functions triggered by events.
With serverless computing, your application still runs on servers, but all the server management is done by AWS.

## Lambda functions:

- Consist of code and any associated dependencies.
- Configuration information is associated with the function.
- You specify the configuration information when you create the function.
- API provided for updating configuration data.

## Lambda Function URL:
A function URL is a dedicated HTTP(S) endpoint for your Lambda function. You can create and configure a function URL through the Lambda console or the Lambda API. 
Lambda function URLs use resource-based policies for security and access control. Function URLs also support cross-origin resource sharing (CORS) configuration options.
- Use Cases:
  - Prototyping an API
  - creating Webhooks
  - For Long running tasks: timeout up to 15 minutes (no more limited to API Gateway)

- Limitations:
   - No specified routes or payload formatting options (your endpoint will be called for each HTTP method)
   - No custom domain names
   - IAM authorization or public endpoints only, no authorizers.
   - Only synchronous invocation
- Secure Lambda Function URL:
  - You can secure your Lambda Function using IAM Authentication, Means your Lambda Function URL only Accessible by IAM User.
  - To provide user Credentials and access Lambda function URL you can use Postman.
## Event source mappings:
- Lambda is an event-driven compute service where AWS Lambda runs code in response to events such as changes to data in an S3 bucket or a DynamoDB table.
- An event source is an AWS service or developer-created application that produces events that trigger an AWS Lambda function to run.
- You can use event source mappings to process items from a stream or queue in services that don’t invoke Lambda functions directly.
- Supported AWS event sources include:

   - Amazon S3.
   - Amazon DynamoDB.
   - Amazon Kinesis Data Streams.
   - Amazon Simple Notification Service.
   - Amazon Simple Email Service.
   - Amazon Simple Queue Service.
   - Amazon Cognito.
   - AWS CloudFormation.
   - Amazon CloudWatch Logs.
   - Amazon CloudWatch Events.
   - AWS CodeCommit.
   - AWS Config.
   - Amazon Alexa.
   - Amazon Lex.
   - Amazon API Gateway.
   - AWS IoT Button.
   - Amazon CloudFront.
   - Amazon Kinesis Data Firehose.
   - Other Event Sources: Invoking a Lambda Function On Demand.

## Lambda Versions:
- Versioning means you can have multiple versions of your function.
- You can use versions to manage the deployment of your AWS Lambda functions.  For example, you can publish a new version of a function for beta testing without affecting users of the stable production version.
- The function version includes the following information:
  - The function code and all associated dependencies.
  - The Lambda runtime that executes the function.
  - All the function settings, including the environment variables.
  - A unique Amazon Resource Name (ARN) to identify this version of the function.
  - Versions are immutable (code cannot be edited).

## Connect VPC with Lambda Function
- To enable your Lambda function to access resources inside your private VPC, you must provide additional VPC-specific configuration information that includes VPC subnet IDs and security group IDs.
- AWS Lambda uses this information to set up elastic network interfaces (ENIs) that enable your function.
- To Associate a Lambda function to VPC, you must add AWSLambdaVPCAccessExecutionRole managed policy to lambda's execution role.

## Lambda Function Alias:
A Lambda alias is a pointer to a function version that you can update. The function's users can access the function version using the alias Amazon Resource Name (ARN).
When you deploy a new version, you can update the alias to use the new version, or split traffic between two versions.
- Aliases can also be used to split traffic between Lambda versions (blue/green).

## Lambda Handler:
- 
