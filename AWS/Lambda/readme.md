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

## Connect VPC with Lambda Function
- To enable your Lambda function to access resources inside your private VPC, you must provide additional VPC-specific configuration information that includes VPC subnet IDs and security group IDs.
- AWS Lambda uses this information to set up elastic network interfaces (ENIs) that enable your function.
- To Associate a Lambda function to VPC, you must add AWSLambdaVPCAccessExecutionRole managed policy to lambda's execution role.

## Lambda Function Alias:
A Lambda alias is a pointer to a function version that you can update. The function's users can access the function version using the alias Amazon Resource Name (ARN).
When you deploy a new version, you can update the alias to use the new version, or split traffic between two versions.
