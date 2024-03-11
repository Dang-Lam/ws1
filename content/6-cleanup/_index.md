---
title : "Clean up resources"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b>6. </b>"
---

We'll take the following steps to delete the resources we created in this exercise.


#### Delete CloudFront

1. Go to  [AWS CloudFront console](https://console.aws.amazon.com/cloudfront/v4/home?region=us-east-1).
  + Click **Distributions**.
  + Click **Delete** and choose delete again

#### Delete Lambda Function
1. Go to [AWS Lambda console](https://console.aws.amazon.com/lambda/home?region=us-east-1)
   + Click chọn các **Functions** ta đã tạo 
   + Click **Actions** -> **Delete** -> Nhập delete và chọn **Delete**
#### Delete Role   
1. Delete [AWS IAM console](https://console.aws.amazon.com/iam/home?region=us-east-1)
   + Click **roles**, **delete** which role created 
   + In **Policies**, filter by Type  **Customer managed** and delete which policy created
#### Delete EC2 Instance
1. Go to [AWS EC2 console](https://console.aws.amazon.com/ec2/v2/home)
   + Click **Instances**.
   + Choose instances.
   + Click **Instance state**.
   + Click **Terminate instance**, then click **Terminate** to confirm.