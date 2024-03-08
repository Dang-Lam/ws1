---
title : "Tạo IAM Role"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

### Tạo IAM Role

Trước tiên cần tạo IAM Policy 
1. Truy cập vào [giao diện quản trị dịch vụ IAM](https://console.aws.amazon.com/iamv2/)
2. Ở thanh điều hướng bên trái, click  **Policies** -> Create policy  
Chọn **JSON tab** và copy code ở file này vào 
![policy](/images/2.prerequisite/038-iamrole.png)

3. Click roles và chọn **Create role**.  

![role1](/images/2.prerequisite/039-iamrole.png)

4. Click **AWS service** và click **Lambda**. 
  + Click **Next**.  

![role1](/images/2.prerequisite/040-iamrole.png)

5. Trong ô Search, điền **AWSLambdaBasicExecutionRole** và policy ta vừa tạo phía trên và ấn phím Enter để tìm kiếm policy này.
  + Click chọn policy **AWSLambdaBasicExecutionRole** và policy vừa tạo
  + Click **Next**
![policy](/images/2.prerequisite/041-iamrole.png)

6. Kiểm tra lại policy đã add đủ chưa và chọn **Create role**

![createrole](/images/2.prerequisite/042-iamrole.png)

Tiếp theo chúng ta sẽ tạo hàm **Lambda** để start/stop **EC2 instance**