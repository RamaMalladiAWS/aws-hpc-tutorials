+++
title = "g. Attach an IAM Role to Lambda"
date = 2019-09-18T10:46:30-04:00
weight = 180
tags = ["tutorial", "serverless", "ParallelCluster", "Lambda", "Slurm"]
+++

{{% notice info %}}
The IAM changes we are conducting here with the AWS Console can also be using Cloudformation like in [*section b*](/04-serverless/02-iam-policy-serverless.html) or with the [AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/iam/index.html). There are always multiple options for you to interest with services in the cloud. Feel free to explore them.
{{% /notice %}}

{{% notice warning %}}
Remember the bucket you crated in [**section b**](/04-serverless/02-iam-policy-serverless.html)? We will need its name for the following steps.
{{% /notice %}}

By default, AWS Lambda create an execution role with permissions to upload logs to [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) Logs. You can customize this default role later when adding triggers. In this case we will add an additional Policy to this role for the Lambda function to execute the scheduler (Slurm) commands using AWS Systems Manager (SSM).