# BYU-AWS-Documentation
All documentation is in reference to the new account structure. 

## Contents
- [Accessing BYU AWS Console](#accessing-byu-aws-console)
- [Accessing BYU AWS CLI](#accessing-byu-aws-cli)
- [Regions to use](#regions-to-use)
- [Tagging Standard](#tagging-standard)
- [Compliance](#compliance)
- [Account Structure](#account-structure)
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
At BYU the primary AWS region that we develop in is us-west-2 or Oregon. If your use case requires it you may also develop in the us-east-1 or Virginia region. If you need access to a region outside of the two provided [contact the cloud office](#contact-the-cloud-office). We chose to use the Oregon region for shorter latency but also provide Virginia so that developers can take advantage of new releases by Amazon. 

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
     * **public:** Information which may, or must, be available to the public and has been formally approved for public release. Examples include Course catalog, Directory, University stats.
     * **internal:** Information which is generally accessible within the University to those employees with a legitimate university purpose; and must be protected against unauthorized use, access, disclosure, acquisition, modification, loss, or deletion. Examples include: organization charts, university policies, student records.
     * **confidential (default):** Information which requires special handling and controls specific to each work environment that limit access and use; and is considered by the University’s senior management to be private and confidential; and must be protected against unauthorized use, access, disclosure, acquisition, modification, loss, or deletion. Examples include: contracts, non-disclosure agreements, donor contact information. 
     * **highly confidential:** Information which requires the strictest rules of handling and usage; is protected and/or regulated by statutes, policies, or regulations; and may also include information for which an Information Trustee has exercised his or her right to restrict access. Examples include: social security numbers, medical records, passwords.
     
        Classification obtained from [University Information Classification](https://infohub.byu.edu/resources/classification/summary).
     
     
* **repo:** URL of the source repository from which resource is being created with a format mimicking "https://github.com/byu-oit/byu-acs" or in other words "https://github.com/organization/repo".

Each tag has a critical purpose for our automation and compliance efforts. Because of this, tagging is enforced in all dev accounts see [Compliance](#compliance) for more information. While tagging is not enforced in production accounts slack alerts will be sent if your resources are not tagged correctly.

## Compliance 

We use a tool called DivvyCloud to check against and remediate security threats as well as to manage compliance in our accounts. In order for an auto remediated action to go live in our AWS accounts a proposal must be made and approved. You can look at the approved proposals in this [box folder](https://byu.box.com/s/doojjaxqfmoe8jergsoi9s4st2ld4xho). 

Here are a list of compliance checks currently running in our AWS accounts:
* Notify of EC2 instances that require patching.
* Notify of encryption keys without key rotation.
* Remediate against globally exposed ports (example SSH open to the world).
* Remediate if CloudTrail logging is disabled.
* Notify if network traffic logs are disabled.
* Notify if root access keys are created.
* Notify if multi-factor authentication is disabled on the account.
* Notify if there is a broken route in a route table.
* Remediate against publicly exposed S3 buckets (if the website flag is set on the public S3 bucket it will not be remediated).
* Notify if a sensitive data volume is not encrypted.
* Notify of stale keys for an IAM user.
* Notify if password policy for account is sub-standard. 

Approved and coming soon:
Off-hours in development and training accounts
* EC2 and RDS instances with the env tag set to "dev", "stg", or "trn" will be turned off at 7pm and turned back on at 7 am. This is done to help minimize wasted cost. This will only be implemented in the byu-trn account and the byu-dev accounts. If your resource should not be turned off you can set your env tag to "dev-noshutdown" or "stg-noshutdown". 
* Tagging Compliance: in order to help keep our accounts organized and also to prevent "junk" compliance checks will be run to make sure resources are tagged with the appropriate tags.
    * Dev and trn accounts: resources that are not tagged correctly will be turned off.
    * Prd accounts: A report will be sent to slack notifying that resources are not tagged appropriately.

## Account Structure

As we have worked to improve the way we use AWS it became clear to use that the way we architected our accounts was not sustainable. In order to better use our resources as well as to simplify work for the Cloud Office as well as developers we restructured. If your account name begins with byu- you are part of the new account structure. Congrats! If you currently do not have an account in the new structure you can order one [here](https://it.byu.edu/it?id=sc_cat_item&sys_id=65d696fadb4bb7800d802c86059619be). All architecture discussed here is in reference to the new account structure.

Accounts are project or product based. Each production account will have an associated development account. A central VPC account will be maintained for VPCs for each use case. These VPCs are then shared to the associated account. This is a huge benefit as it allows VPCs to be managed from one location. It also allows us to manage less VPCs as a new VPC is not required for each account made. Finally it allows us to better use our limited network space. VPCs cannot be edited or modified from shared accounts. Aside from account administrators you will not have access to create other VPCs. If you have a use case that requires a specialized VPC contact the [Cloud Office](#contact-the-cloud-office).

The following is an architecture diagram of what our VPCs look like.
![VPC Diagram](/images/vpcDiagram.png)

The following is an architecture diagram of what our account structure looks like.
![Account Diagram](/images/accountStructure.png)

Diagrams created by Josh Gubler.

Thank you for your patience as we move to this new structure. We believe that it will be a benefit to all involved and that the effort of moving will be worth it in the long run. If you have questions and concerns you can contact the [Cloud Office](#contact-the-cloud-office).

## Service Control Policies

## Permission Boundaries

## Contact the Cloud Office
The Cloud Office is here to help you! We want our AWS accounts to enable you to do your work. If there are any policies mentioned above that do not work for your use case please contact us! If you have questions, concerns, or feedback please do not hesitate to reach out to the Cloud Office. 

You can contact the Cloud Office through byu-oit.slack.com in the #cloud-office channel, by @cloud-office in slack, or by emailing cloudoffice@byu.edu. A Cloud Office website will be coming soon. 

If you have general aws questions or comments you can post through byu-oit.slack.com in the #aws channel.

If you would like to get advice from other developers you can ask questions in the #aws-swat channel. 
