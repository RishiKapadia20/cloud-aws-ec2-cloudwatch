# AWS - EC2 CloudWatch Opspack

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers and send metrics to CloudWatch for your EC2 instances making AWS Monitoring Simple.

## What Can You Monitor

Opsview Monitor's AWS EC2 Opspack helps detect issues within your EC2 instance. Opsview provides all of the latest service checks to make sure your EC2 instance is up and running. The EC2 credit usage and balance show the number of CPU credits consumed and available.

Note: This Opspack knows when it was last run, so when testing the results in the troubleshoot section, you will need to wait a couple minutes each time you recheck the results. The time frame that is searched for is based around the last time the Opspack ran, so running it too quickly will result in no data being found and the service check going into an unknown.

## Service Checks

| Service Check | Description |
|:------------- |:----------- |
|AWS/EC2.CPUCreditUsage | Must be T2 instance. The number of CPU credits consumed
|AWS/EC2.CPUCreditBalance | Must be T2 instance. The number of CPU credits available
|AWS/EC2.CPUUtilization | The percentage of allocated EC2 units that are in use
|AWS/EC2.DiskReadOps | The number of completed read operations
|AWS/EC2.DiskWriteOps | The number of completed write operations
|AWS/EC2.DiskWriteBytes | Bytes written to all instance store volumes available to the instance
|AWS/EC2.DiskReadBytes | Bytes read from all instance store volumes available to the instance
|AWS/EC2.NetworkIn | The number of bytes received by the instance
|AWS/EC2.NetworkOut | The number of bytes sent out on all network interfaces by the instance
|AWS/EC2.NetworkPacketsIn | The number of packets received on all network interfaces by the instance
|AWS/EC2.NetworkPacketsOut |The number of packets sent out on all network interfaces by the instance
|AWS/EC2.StatusCheckFailed | Reports whether the instance has passed both the instance status check and the system status check

## Prerequisites

To be able to monitor AWS CloudWatch services you need to add your AWS credentials to your Opsview Monitor server.

We recommend adding your AWS Access Key ID and AWS Secret Key ID to the default location:

 `/opt/opsview/monitoringscripts/etc/plugins/cloud-aws/aws_credentials.cfg`

This credentials file should be in the following format:

```
[default]
aws_access_key_id = "Your Access Key Id"
aws_secret_access_key = "Your Secret Key Id"
```

If you are not using the default path, you will then need to assign your path to the variable: `AWS_CLOUDWATCH_AUTHENTICATION`.

## Setup and Configuration

To configure and utilize this Opspack, you need to add the 'Cloud - AWS - EC2 CloudWatch' Opspack to the host running the EC2 software.

#### Step 1: Add the host template

Note: For the hostname field, you can either supply the Public DNS name of the instance or add the instance ID to the `AWS_EC2_INSTANCE_ID` variable.

Note: If you supply both the Public DNS name and the Instance ID, then add the -p option to the Host Address to activate the mode to check that the public DNS name and instance ID match.

![Add host template](/docs/img/add_aws_ec2_host.png?raw=true)

#### Step 2: Add and configure the variables for the host

* `AWS_CLOUDWATCH_AUTHENTICATION` - Contains either the file location created earlier (recommended method) or add the Access Key and Secret Key directly to this variable's values.

* Override the Region value if you are not using the default

![Add credentials variable](/docs/img/add_aws_credentials_variable.png?raw=true)

* `AWS_EC2_INSTANCE_ID` - The Instance ID from AWS EC2

![Add instance variable](/docs/img/add_ec2_instance_variable.png?raw=true)

#### Step 3: Reload and view the EC2 statistics

![View service checks](/docs/img/view_aws_ec2_service_checks.png?raw=true)
