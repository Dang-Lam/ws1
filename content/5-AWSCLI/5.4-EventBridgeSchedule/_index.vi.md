---
title : "Tạo EventBridge Schedule"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 5.4 </b> "
---

Tạo file **Scheduler-Execution-Role.json** với nội dung

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

Từ AWS Command Line interface (AWS CLI), điền câu lệnh sau để tạo new role mới. 

```bash
aws iam create-role \
    --role-name SchedulerExecutionRole \
    --assume-role-policy-document file://Scheduler-Execution-Role.json
```

Nếu thành công ta có output:

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

Tạo file `PermissionPolicy.json` với nội dung sau

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

Chạy câu lệnh sau để tạo một policy mới:

```bash
 aws iam create-policy \
    --policy-name lambda_function_startEC2Inc \
    --policy-document file://PermissionPolicy.json
```

Ta có output:

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

Chạy câu lệnh sau để gán policy vào role của bạn. 

```bash
aws iam attach-role-policy \
    --policy-arn arn:aws:iam::339713042597:policy/lambda_function_startEC2Inc \
    --role-name SchedulerExecutionRole
```

Tạo eventbridge schedule theo câu lệnh sau:

```bash
aws scheduler create-schedule \
    --name StopEC2Instances_CLI  \
    --schedule-expression 'rate(5 minutes)' \
    --target '{"RoleArn": "arn:aws:iam::339713042597:role/SchedulerExecutionRole", "Arn": "arn:aws:lambda:us-east-1:339713042597:function:function_startec2instances"}' \
    --flexible-time-window '{ "Mode": "OFF"}'
```


{{% notice info %}}
 RoleArn là địa chỉ arn của Role **SchedulerExecutionRole**, Arn là địa chỉ arn của function **function_startec2instances**
{{% /notice %}}

Khi hoàn thành sẽ trả output:

```json
{
    "ScheduleArn": "arn:aws:scheduler:us-east-1:339713042597:schedule/default/StopEC2Instances_CLI"
}

```

Với schedule stop ta cũng làm tương tự như trên