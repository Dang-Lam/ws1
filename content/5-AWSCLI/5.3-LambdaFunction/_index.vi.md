---
title : "Tạo Lambda Function"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 5.3 </b> "
---

Tạo file **function_startec2instances.py** 

```python
import boto3
region = 'us-east-1'
instances = ['i-0c899a57eb77e26a0','i-072bcd2e760962f7f']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.start_instances(InstanceIds=instances)
    print('started your instances: ' + str(instances))

```

Nén file .py thành đuôi .zip

```
7z a -tzip function_startec2instances.zip function_startec2instances.py
```

Tạo function với cấu trúc sau:

```
aws lambda create-function\
    --function-name function_startec2instances\`Enter your function name here`
    --runtime python3.9\`Enter the correct runtime identifier here`
    --zip-file fileb://function_startec2instances.zip\`Enter the location of your zipped lambda function code`
    --handler function_startec2instances.lambda-handler\`Enter the identifier for the handler function in your Python app`
    --role arn:aws:iam::745198902022:role/lambda-basic-role `Enter the role Arn you saved earlier`

```
Ta có câu lệnh sau:
```
aws lambda create-function \
    --function-name function_startec2instances \
    --zip-file fileb://function_startec2instances.zip --handler function_startec2instances.lambda_handler --runtime python3.9 \
    --role arn:aws:iam::339713042597:role/Lambda_start+stop_cli
```

Kiểm tra trạng thái của instance

```
aws ec2 describe-instances \
    --filters Name=instance-state-name,Values=* \
    --query 'Reservations[].Instances[*].{InstanceType: InstanceType, InstanceId: InstanceId, State: State.Name}' \
    --profile lab --output table
```

Ta có output:

```
----------------------------------------------------
|                 DescribeInstances                |
+----------------------+----------------+----------+
|      InstanceId      | InstanceType   |  State   |
+----------------------+----------------+----------+
|  i-0c81fc6f81b66ad43 |  t2.micro      |  stopped |
|  i-0c899a57eb77e26a0 |  t2.micro      |  stopped |
|  i-072bcd2e760962f7f |  t2.micro      |  stopped |
|  i-08fab453c4c75f370 |  t2.micro      |  stopped |
|  i-0618ac398923f1c1f |  t2.micro      |  stopped |
|  i-0b24b39e574d2cc5b |  t2.micro      |  stopped |
+----------------------+----------------+----------+
```

Chạy test function với câu lệnh:

```
aws lambda invoke \
    --function-name   function_startec2instances out \ 
    --log-type Tail
```

Ta có output hiển thị như sau:

```
{
    "StatusCode": 200,
    "LogResult": "U1RBUlQgUmVxdWVzdElkOiBmODhkNDdkOS04YTlmLTRhMmMtODE0My1mYzBkZmI1NWZlOGIgVmVyc2lvbjogJExBVEVTVApzdGFydGVkIHlvdXIgaW5zdGFuY2VzOiBbJ2ktMGM4OTlhNTdlYjc3ZTI2YTAnLCAnaS0wNzJiY2QyZTc2MDk2MmY3ZiddCkVORCBSZXF1ZXN0SWQ6IGY4OGQ0N2Q5LThhOWYtNGEyYy04MTQzLWZjMGRmYjU1ZmU4YgpSRVBPUlQgUmVxdWVzdElkOiBmODhkNDdkOS04YTlmLTRhMmMtODE0My1mYzBkZmI1NWZlOGIJRHVyYXRpb246IDE3NTYuMzIgbXMJQmlsbGVkIER1cmF0aW9uOiAxNzU3IG1zCU1lbW9yeSBTaXplOiAxMjggTUIJTWF4IE1lbW9yeSBVc2VkOiA4NCBNQgkK",
    "ExecutedVersion": "$LATEST"
}

```

Kiểm tra lại trạng thái instance bằng câu lệnh lúc nãy ta có output:

```
----------------------------------------------------
|                 DescribeInstances                |
+----------------------+----------------+----------+
|      InstanceId      | InstanceType   |  State   |
+----------------------+----------------+----------+
|  i-0c81fc6f81b66ad43 |  t2.micro      |  stopped |
|  i-0c899a57eb77e26a0 |  t2.micro      |  running |
|  i-072bcd2e760962f7f |  t2.micro      |  running |
|  i-08fab453c4c75f370 |  t2.micro      |  stopped |
|  i-0618ac398923f1c1f |  t2.micro      |  stopped |
|  i-0b24b39e574d2cc5b |  t2.micro      |  stopped |
+----------------------+----------------+----------+
```

2 instance đã được running thành công
