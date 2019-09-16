# BYU-AWS-Documentation

## Contents
- [Accessing BYU AWS Console](#accessing-byu-aws-console)
- [Accessing BYU AWS CLI](#accessing-byu-aws-cli)
- [Regions to use](#regions-to-use)
- [Tagging Standard](#tagging-standard)
- [Compliance](#compliance)
- [Account Structure](#account-structure)
- [Training Account](#training-account)
- [Development Accounts](#development-accounts)
- [Production Accounts](#production-accounts)
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
At BYU the primary AWS region that we develop in is us-west-2 or Oregon. If your use case requires it you may also develop in the us-east-1 or Virginia region. If you need access to a region outside of the two provided contact the cloud office - [Contact the Cloud Office](#contact-the-cloud-office). We chose to use the Oregon region for shorter latency but also provide virginia so that developers can take advantage of new releases by Amazon. 

AWS logs you into a random region upon your first login. To change the region in the console go to the top right hand corner of the page and select the region dropdown. In the CLI you specify a default region in the AWS CLI using either the aws configure command or the AWS_DEFAULT_REGION environment variable. For more information, see [Configuring the AWS Region](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-installing-specifying-region) in the AWS Command Line Interface User Guide.

It is a good idea to check what region you are in every time you log into the console.

## Tagging Standard

We implemented a tagging standard at BYU for organization and automation efforts. The tagging standard is described below...

* **env:**
     * **trn:** For training, learning, or experimental efforts (should be used for the byu-trn account).
     * **dev-noshutdown:** A development system that should not be part of our off-hours scheduling.
     * **tst:** Automated testing
     * **stg:** Staging systems used for QA and User Acceptance Testing
     * **stg-noshutdown:** A staging system that should not be part par of our off-hours scheduling.
     * **prd:** Production
     
     
* **data-sensitivity:**
     * **public:** Information which may, or must, be available to the public and has been formally approved for public release. Examples:include Course catalog, Directory, University stats.
     * **internal:** Information which is generally accessible within the University to those employees with a legitimate university purpose; and must be protected against unauthorized use, access, disclosure, acquisition, modification, loss, or deletion. Examples include: organization charts, university policies, student records.
     * **confidential (default):** Information which requires special handling and controls specific to each work environment that limit access and use; and is considered by the University’s senior management to be private and confidential; and must be protected against unauthorized use, access, disclosure, acquisition, modification, loss, or deletion. Examples include: contracts, non-disclosure agreements, donor contact information. 
     * **highly confidential:** Information which requires the strictest rules of handling and usage; is protected and/or regulated by statutes, policies, or regulations; and may also include information for which an Information Trustee has exercised his or her right to restrict access. Examples include: social security numbers, medical records, passwords.
     
Classification obtained from [University Information Claasification](https://infohub.byu.edu/resources/classification/summary).
     
     
* **repo:**

Each tag has an important purpose. Because of this tagging is enforced in all dev accounts see [Compliance](#compliance) for more information. While tagging is not enforced in production accounts slack alerts will be sent if your resources are not tagged correctly.

## Compliance 

## Account Structure
![Account Diagram](/images/accountStructure.png)
![VPC Diagram](/images/vpcDiagram.png)

## Training Account

## Development Accounts

## Production Accounts

## Service Control Policies

## Permission Boundaries

## Contact the Cloud Office
