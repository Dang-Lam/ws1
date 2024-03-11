---
title : "Tạo IAM Role"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

1. Tạo **AWS IAM Policy**
  + Tạo file **lambda_stop+start.json**

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
  + Chạy câu lệnh 
  ```aws iam create-policy \
    --policy-name lambda_stop+start_cli \
    --policy-document file://lambda_stop+start.json
```

![policy](/images/5.fwd/001-fwd.png) 

1. Tạo **IAM Role**
  + Trong case này, chúng ta sẽ tạo một role để dịch vụ Lambda đảm nhận. Tạo một trust policy cho phép Lambda đảm nhận role này.
  + Tạo file **trust-policy.json**
  + Để tạo một **IAM role**, mở terminal tại đường dẫn chứa file và sử sụng câu lệnh **create-role**
  
  ```aws iam create-role --role-name Lambda_start+stop_cli --assume-role-policy-document file://trust-policy.json```


![CreateRole](/images/5.fwd/002-fwd.png) 

  + Gán **Managed Policy** tới một **IAM role** với **AWS CLI** 

    Managed Policy có 2 loại:
      + **AWS-managed policies** - được tạo và quản lý bởi AWS
      + **Customer-managed policies** - được tạo và quản lý bởi user
  + Để attach một AWS-managed policy **AWSLambdaBasicExecutionRole** vào IAM role với AWS CLI, sử dụng **attach-role-policy** 
  
  ```aws iam attach-role-policy --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole --role-name Lambda_start+stop_cli```
![CreateRole](/images/5.fwd/003-fwd.png) 
  Tương tự lấy policy-arn mà mình vừa tạo ở trên để  gán vào role  Lambda_start+stop_cli

  ```aws iam attach-role-policy --policy-arn arn:aws:iam::339713042597:policy/lambda_stop+start_cli --role-name Lambda_start+stop_cli```

  Kiểm tra lại Policy đã chính xác chưa
  ```aws iam list-attached-role-policies --role-name Lambda_start+stop_cli```
![CheckPermission](/images/5.fwd/004-fwd.png) 