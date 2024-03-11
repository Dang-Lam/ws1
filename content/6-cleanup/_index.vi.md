---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

Chúng ta sẽ tiến hành các bước sau để xóa các tài nguyên chúng ta đã tạo trong bài thực hành này.


#### Xóa CloudFront

1. Truy cập [giao diện quản trị dịch vụ CloudFront](https://console.aws.amazon.com/cloudfront/v4/home?region=us-east-1).
  + Click chọn **Distributions** đã tạo.
  + Click **Delete** và chọn 1 lần nữa để xóa

### Xóa Lambda Function
2. Truy cập [giao diện quản trị dịch vụ Lambda](https://console.aws.amazon.com/lambda/home?region=us-east-1)
   + Click chọn các **Functions** ta đã tạo 
   + Click **Actions** -> **Delete** -> Nhập delete và chọn **Delete**
### Xóa Role   
3. Truy cập [giao diện quản trị dịch vụ IAM](https://console.aws.amazon.com/iam/home?region=us-east-1)
   + Click chọn **roles**, **delete** những role ta đã tạo 
   + Tương tự, trong **Policies**, ta filter by Type bằng **Customer managed** và xóa những policy đã tạo
### Xóa EC2 Instance
4. Truy cập [giao diện quản trị dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home)
   + Click **Instances**.
   + Chọn instances đã tạo.
   + Click **Instance state**.
   + Click **Terminate instance**, sau đó click **Terminate** để xác nhận.