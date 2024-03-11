---
title : "Create IAM Role"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

1. Create **AWS IAM Policy**
  + Create file **lambda_stop+start.json**
    ```json
      {
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


  + Run Command

    ```aws iam create-policy \
    --policy-name lambda_stop+start_cli \
    --policy-document file://lambda_stop+start.json
    ```

  ![policy](/images/5.fwd/001-fwd.png) 

1. Create **IAM Role**
  + In this case, We will create a role for the Lambda service to take on. Create a trust policy that allows Lambda to take on this role.
  + Create file **trust-policy.json**
  + To create **IAM role**, Open terminal at the path containing the file and use the command **create-role**
  
    ```
    aws iam create-role \
      --role-name Lambda_start+stop_cli \
      --assume-role-policy-document file://trust-policy.json
    ```

  ![CreateRole](/images/5.fwd/002-fwd.png) 

  + Attach **Managed Policy** to an **IAM role** with **AWS CLI** 

    Managed Policy has 2 type:
      + **AWS-managed policies** - created and managed by AWS
      + **Customer-managed policies** - created and managed by user
  + To attach an AWS-managed policy **AWSLambdaBasicExecutionRole** in IAM role with AWS CLI, using **attach-role-policy** 
  
    ```
    aws iam attach-role-policy \
      --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole \
      --role-name Lambda_start+stop_cli
    ```
  ![CreateRole](/images/5.fwd/003-fwd.png) 
  Again pick up policy-arn attach to role  Lambda_start+stop_cli

    ```
    aws iam attach-role-policy \
      --policy-arn arn:aws:iam::339713042597:policy/lambda_stop+start_cli \
      --role-name Lambda_start+stop_cli
    ```
  Check if the Policy is correct
    ```aws iam list-attached-role-policies \ 
      --role-name Lambda_start+stop_cli
    ```
  ![CheckPermission](/images/5.fwd/004-fwd.png) 