# AWS Config
- AWS Config is a fully managed service that provides you with an AWS resource inventory, configuration history, and configuration change notifications to enable security and governance.
- With AWS Config you can discover existing AWS resources, export a complete inventory of your AWS resources with all configuration details, and determine how a resource was configured at any point in time.
- These capabilities enable compliance auditing, security analysis, resource change tracking, and troubleshooting.
- Allow you to assess, audit and evaluate configurations of your AWS resources.

## AWS Config VS AWS Cloudtrail:
- AWS CloudTrail records user API activity on your account and allows you to access information about this activity.
- AWS Config records point-in-time configuration details for your AWS resources as Configuration Items (CIs).
- You can use an AWS Config CI to answer, “What did my AWS resource look like?” at a point in time.
- You can use AWS CloudTrail to answer, “Who made an API call to modify this resource?”.

## AWS Config Rules:
- A Config Rule represents desired configurations for a resource and is evaluated against configuration changes on the relevant resources, as recorded by AWS Config.
- AWS Config Rules can check resources for certain desired conditions and if violations are found the resources are flagged as “noncompliant”.
- Used to check like:
  - Is backup enabled on Amazon RDS?
  - Is CloudTrail enabled on the AWS account?
  - Are Amazon EBS volumes encrypted.
 
## AWS Config Remediation:
- AWS Config allows you to remediate noncompliant resources that are evaluated by AWS Config Rules.
- AWS Config applies remediation using AWS Systems Manager Automation documents. These documents define the actions to be performed on noncompliant(mis.-configuration) AWS resources evaluated by AWS Config Rules.
