# BYU-AWS-Documentation

## Contents
- [Accessing BYU AWS Console](#accessing-byu-aws-console)
- [Accessing BYU AWS CLI](#accessing-byu-aws-cli)
- [Regions to use](#regions-to-use)
- [Tagging Standard](#tagging-standard)
- [Compliance](#compliance)
- [Account Structure](#account-structure)
- [Training Account](#training-account)
- [Service Control Policies](#service-control-policies)
- [Permission Boundaries](#permission-boundaries)
- [Contact the Cloud Office](#contact-the-cloud-office)

## Accessing BYU AWS Console
1. Go to awslogin.byu.edu
2. Sign in with NetID and password.
3. Authenticate with DUO.

## Accessing BYU AWS CLI
1. Download awslogin: https://github.com/byu-oit/awslogin.git
2. Sign in with NetID and password.
3. Authenticate with DUO (It is recommended that you have DUO automatically send you a push if you will be using the AWS CLI).

## Regions to use
At BYU the primary AWS region that we develop in is us-west-2 or Oregon. If your use case requires it you may also develop in the use-east-1 or Virginia region. If you need access to a region outside of the two provided contact the cloud office - [Contact the Cloud Office](#contact-the-cloud-office). 

AWS logs you into a random region upon your first login. To change the region in the console go to the top right hand corner of the page and select the region dropdown. In the CLI you specify a default region in the AWS CLI using either the aws configure command or the AWS_DEFAULT_REGION environment variable. For more information, see [Configuring the AWS Region](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-installing-specifying-region) in the AWS Command Line Interface User Guide.

## Tagging Standard

## Compliance 

## Account Structure
![Account Diagram](/images/accountStructure.png)
![VPC Diagram](/images/vpcDiagram.png)

## Training Account

## Service Control Policies

## Permission Boundaries

## Contact the Cloud Office
