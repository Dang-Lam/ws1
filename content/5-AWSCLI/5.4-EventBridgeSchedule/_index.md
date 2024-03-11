---
title : "Tạo EventBridge Schedule"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 5.4 </b> "
---

Create file **Scheduler-Execution-Role.json** 

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "scheduler.amazonaws.com"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

From the AWS Command Line interface (AWS CLI), enter the following command to create a new role. 

```bash
aws iam create-role \
    --role-name SchedulerExecutionRole \
    --assume-role-policy-document file://Scheduler-Execution-Role.json
```

If successful, we have output:

```
{
    "Role": {
        "Path": "/",
        "RoleName": "SchedulerExecutionRole",
        "RoleId": "AROAU6GDZVCSVY2OKGS2M",
        "Arn": "arn:aws:iam::339713042597:role/SchedulerExecutionRole",
        "CreateDate": "2024-02-29T08:09:09+00:00",
        "AssumeRolePolicyDocument": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Principal": {
                        "Service": "scheduler.amazonaws.com"
                    },
                    "Action": "sts:AssumeRole"
                }
            ]
        }
    }
}

```

Create file `PermissionPolicy.json` with the following content

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lambda:InvokeFunction"
            ],
            "Resource": [
                "arn:aws:lambda:us-east-1:339713042597:function:function_startec2instances:*",
                "arn:aws:lambda:us-east-1:339713042597:function:function_startec2instances"
            ]
        }
    ]
}
```

Run the following command to create a new policy:

```bash
 aws iam create-policy \
    --policy-name lambda_function_startEC2Inc \
    --policy-document file://PermissionPolicy.json
```

We have output:

```json
{
    "Policy": {
        "PolicyName": "lambda_function_startEC2Inc",
        "PolicyId": "ANPAU6GDZVCS46LWRELGH",
        "Arn": "arn:aws:iam::339713042597:policy/lambda_function_startEC2Inc",
        "Path": "/",
        "DefaultVersionId": "v1",
        "AttachmentCount": 0,
        "PermissionsBoundaryUsageCount": 0,
        "IsAttachable": true,
        "CreateDate": "2024-02-29T08:22:38+00:00",
        "UpdateDate": "2024-02-29T08:22:38+00:00"
    }
}

```

Run the following command to assign the policy to your role.

```bash
aws iam attach-role-policy \
    --policy-arn arn:aws:iam::339713042597:policy/lambda_function_startEC2Inc \
    --role-name SchedulerExecutionRole
```

Create eventbridge schedule with the following command:

```bash
aws scheduler create-schedule \
    --name StopEC2Instances_CLI  \
    --schedule-expression 'rate(5 minutes)' \
    --target '{"RoleArn": "arn:aws:iam::339713042597:role/SchedulerExecutionRole", "Arn": "arn:aws:lambda:us-east-1:339713042597:function:function_startec2instances"}' \
    --flexible-time-window '{ "Mode": "OFF"}'
```


{{% notice info %}}
 RoleArn is the arn address of Role **SchedulerExecutionRole**, Arn is the arn address of function **function_startec2instances**
{{% /notice %}}

When completed, it will return output:

```json
{
    "ScheduleArn": "arn:aws:scheduler:us-east-1:339713042597:schedule/default/StopEC2Instances_CLI"
}

```

With schedule stop we also do the same as above