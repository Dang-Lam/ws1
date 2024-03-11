---
title : "Create IAM Role"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

### Create IAM Role

First you need to create an IAM Policy
1. Go to [AWS Management Console](https://console.aws.amazon.com/iamv2/)
2. In the left navigation bar, click  **Policies** -> Create policy  
Click **JSON tab** and copy code below: 
  ```{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:*:*:*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:Start*",
        "ec2:Stop*"
      ],
      "Resource": "*"
    }
  ]
}
```

![policy](/images/2.prerequisite/038-iamrole.png)

3. Click roles and choose **Create role**.  

![role1](/images/2.prerequisite/039-iamrole.png)

4. Click **AWS service** và click **Lambda**. 
  + Click **Next**.  

![role1](/images/2.prerequisite/040-iamrole.png)

5. In Search, select  **AWSLambdaBasicExecutionRole** and  policy which created and Enter to pick.
  + Click  policy **AWSLambdaBasicExecutionRole** and policy which created
  + Click **Next**
![policy](/images/2.prerequisite/041-iamrole.png)

1. Check if the policy has been added properly and choose **Create role**

![createrole](/images/2.prerequisite/042-iamrole.png)

Next, we create **Lambda Function** to start/stop **EC2 instance**