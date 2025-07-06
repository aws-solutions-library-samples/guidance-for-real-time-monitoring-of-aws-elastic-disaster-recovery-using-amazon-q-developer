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

### Install Elastic Disaster Recovery Replication Agent on an EC2 instance.

To test the Guidance, install Elastic Disaster Recovery Replication Agent on an EC2 instance.

### Observe CreateSourceServerForDrs in AWS CloudTrail events history.

After the AWS Replication Agent is installed successfully on an EC2 instance, `CreateSourceServerForDrs` CloudTrail event is generated.

### Wait for the delivery of CloudTrail event notification by Amazon Q into your Slack channel.

Amazon Q Developer is subscribed to Amazon SNS Topic. After receiving the CloudWatch event, Amazon Q Dveloper will deliver the event into your Slack channel.

### Build a simple prompt in your Slack channel and ask Amazon Q status of replication status of source servers in Elastic Disaster Recovery service.

In the Slack channel, use a simple prompt such as "**@Amazon Q What is the status of data replication of my source servers in Elastic Disaster Recovery service in Ireland region?**" to interact with Elastic Disaster Recovery resources through simple conversational commands in Slack, without needing to access the AWS Console.

## Next Steps

- Incident tickets can be automatically created and routed to appropriate teams when CloudWatch emits specific events, such as replication stalled events.
- The solution can be deployed at AWS Organizational level montitoring all AWS accounts or a subset of accounts.

## Cleanup

To delete and cleanup deployed resources, use one of the following methods:

- From the [AWS Management Console](https://console.aws.amazon.com) in your web browser, open the CloudFormation console, click **Stacks** on the left-hand menu, select the stack with the name `<STACK_NAME>`, and click **Delete**.
- If AWS CLI is installed, run the following command: 
```
aws cloudformation delete-stack --stack-name <STACK_NAME>
```
