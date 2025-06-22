# Guidance for Real-time monitoring of AWS Elastic Disaster Recovery using Amazon Q Developer

## Table of Contents

1. [Overview](#overview-required)
    - [Architecture](#architecture)
    - [Cost](#cost)
3. [Prerequisites](#prerequisites)
    - [Third-party tools](#third-party-tools)
    - [AWS account requirements](#aws-account-requirements)
    - [Supported Regions](#supported-regions)
4. [Deployment Steps](#deployment-steps)
5. [Deployment Validation](#deployment-validation)
6. [Running the Guidance](#running-the-guidance)
7. [Next Steps](#next-steps)
8. [Cleanup](#cleanup)

***Optional***

8. [FAQ, known issues, additional considerations, and limitations](#faq-known-issues-additional-considerations-and-limitations-optional)
9. [Revisions](#revisions-optional)
10. [Notices](#notices-optional)
11. [Authors](#authors-optional)

## Overview

This solution enables customers to implement comprehensive real-time monitoring and intelligent analysis of their AWS Elastic Disaster Recovery (DRS) environments using Amazon Q Developer. By integrating DRS APIs, CloudWatch metrics, and Q Developer's AI capabilities, this architecture provides seamless visibility into replication health, recovery readiness, and operational insights. Customers can leverage Q Developer's natural language interface to query their DRS environment, analyze server states, and receive intelligent recommendations for optimizing their disaster recovery posture. Rather than relying solely on manual console navigation or basic Amazon CloudWatch dashboards, customers can now interact with their DRS infrastructure through conversational AI that understands disaster recovery concepts and provides contextual guidance. This solution unlocks enhanced DRS monitoring capabilities by enabling customers to gain deeper operational insights and make informed decisions about their disaster recovery strategy through intelligent, real-time analysis powered by Amazon Q Developer.

### Architecture

![reference architecture](assets/guidance-for-real-time-monitoring-of-aws-elastic-disaster-recovery-using-amazon-q-developer.jpg)

### Cost

You are responsible for the cost of the AWS services used while running this Guidance. Amazon Q Developer for chat channels is available at no extra cost under the free tier. The serverless architecture leverages pay-as-you-go services with very low usage costs: Amazon SNS ($0.60 per million notifications) and Amazon EventBridge ($1.00 per million events with free delivery to services in the same account). For a typical deployment monitoring 5-10 servers, the estimated monthly cost would likely be under $1, as you would need to generate hundreds of thousands of events to reach even a single dollar in charges. Even for large environments with dozens or hundreds of servers, monthly costs would typically remain under $5 unless you're implementing extensive logging or custom metrics.

## Prerequisites


### Third-party tools

* A Slack channel (private or public)

### AWS account requirements

* You have source server(s) being protected with Elastic Disaster Recovery service.
* You have authorized Amazon Q Developer to access your Slack workspace.


### Supported Regions

This Guidance can be deployed in all regions mentioned here https://docs.aws.amazon.com/chatbot/latest/adminguide/chatbot-regions.html

## Deployment Steps

1. Make sure you have a Slack channel created and authorized Amazon Q Developer to access your Slack workspace prior to deploying this Guidance.
2. Copy the CloudFormation template provided in the Guidance and deploy via CloudFormation.


## Deployment Validation

To validate deployment, use one or more of the following methods:

* To validate the deployment, open CloudFormation console in your AWS Management Console, click **Stacks** on the left-hand menu, and verify the stack with the name `<STACK_NAME>` has a status of **CREATE_COMPLETE**. After clicking the stack name, click the **Outputs** tab and take note of the **SlackChannelConfigurationArn** and **DRSSlackNotificationTopicArn**.

* If AWS CLI is installed, run the following command to validate the deployment has a status of **CREATE_COMPLETE**, and take note of the **SlackChannelConfigurationArn** and **DRSSlackNotificationTopicArn** output values:
```
aws cloudformation describe-stacks --stack-name <STACK_NAME>
```


## Running the Guidance

<Provide instructions to run the Guidance with the sample data or input provided, and interpret the output received.> 

This section should include:

* Guidance inputs
* Commands to run
* Expected output (provide screenshot if possible)
* Output description



## Next Steps (required)

Provide suggestions and recommendations about how customers can modify the parameters and the components of the Guidance to further enhance it according to their requirements.


## Cleanup (required)

- Include detailed instructions, commands, and console actions to delete the deployed Guidance.
- If the Guidance requires manual deletion of resources, such as the content of an S3 bucket, please specify.



## FAQ, known issues, additional considerations, and limitations (optional)


**Known issues (optional)**

<If there are common known issues, or errors that can occur during the Guidance deployment, describe the issue and resolution steps here>


**Additional considerations (if applicable)**

<Include considerations the customer must know while using the Guidance, such as anti-patterns, or billing considerations.>

**Examples:**

- “This Guidance creates a public AWS bucket required for the use-case.”
- “This Guidance created an Amazon SageMaker notebook that is billed per hour irrespective of usage.”
- “This Guidance creates unauthenticated public API endpoints.”


Provide a link to the *GitHub issues page* for users to provide feedback.


**Example:** *“For any feedback, questions, or suggestions, please use the issues tab under this repo.”*

## Revisions (optional)

Document all notable changes to this project.

Consider formatting this section based on Keep a Changelog, and adhering to Semantic Versioning.

## Notices (optional)

Include a legal disclaimer

**Example:**
*Customers are responsible for making their own independent assessment of the information in this Guidance. This Guidance: (a) is for informational purposes only, (b) represents AWS current product offerings and practices, which are subject to change without notice, and (c) does not create any commitments or assurances from AWS and its affiliates, suppliers or licensors. AWS products or services are provided “as is” without warranties, representations, or conditions of any kind, whether express or implied. AWS responsibilities and liabilities to its customers are controlled by AWS agreements, and this Guidance is not part of, nor does it modify, any agreement between AWS and its customers.*


## Authors (optional)

Name of code contributors
