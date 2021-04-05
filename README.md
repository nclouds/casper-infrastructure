# Casper Node Infrastructure

This repository contains CloudFormation templates to deploy and bootstrap a Casper node on AWS.

## Getting Started

### Quick Start

You can deploy the infrastructure by selecting one of the regions below, and clicking on the *launch stack* button. Follow the instructions on the AWS console and fill the required parameters to deploy the CloudFormation stack.

|Region||
|-|-|
| us-west-2 | [![launch_stack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=casper-0&templateURL=https://nclouds-cloudformation-templates.s3-us-west-2.amazonaws.com/casper/master.packaged.yml&region=us-west-2) |

### Manual Deployment

You can also download the CloudFormation templates and deploy the infrastructure manually using the *[aws-cli](https://aws.amazon.com/cli/)*:

*Note: You should have already installed and configured the aws cli in order to follow these steps*

1. Create an S3 Bucket to store the CloudFormation templates.
2. Package and upload the templates to S3:

    ```console
    $ aws cloudformation package \
        --template-file master.yml \
        --output-template-file master.packaged.yml \
        --s3-bucket <YOUR_S3_BUCKET>
    ```

3. Create the CloudFormation stack:

    ```console
    $ aws cloudformation deploy \
        --template-file master.packaged.yml \
        --stack-name <STACK_NAME>   
    ```

    Choose a meaningful name for you CloudFormation Stack and deploy the infrastructure.

### Monitoring the Node

An AWS CloudWatch dashboard is created as part of the infrastructure with some metrics about the node. You can access the dashboard using the [CloudWatch console](https://console.aws.amazon.com/cloudwatch/home?#dashboards:) or by opening the URL of the dashboard in the CloudFormation stack outputs.

### Accessing the Node

You can securely access the node using AWS Session Manager by opening the [console](https://console.aws.amazon.com/systems-manager/session-manager/sessions) and clicking on *Start Session*, then just select your instance and you will get access to the node through a terminal embbeded in the browser. *(Note: You can also access the node through your terminal by using the aws cli and the session manager plugin)*

### Delete Resources

To completely delete all the resources created by the templates go to the [CloudFormation Console](https://console.aws.amazon.com/cloudformation/home), select your stack and delete it.

![delete-stack](images/delete-stack.png)


## Infrastructure

![casper](images/casper.png)

The CloudFormation templates create the following components as part of the infrastructure:

- A VPC with public and private subnets, and all the routing configuration.
- A single instance Auto Scaling Group that bootstraps a Casper node.
- A CloudWatch dashboard with metrics to monitor the node.
- Configuration to access the node through Session Manager.