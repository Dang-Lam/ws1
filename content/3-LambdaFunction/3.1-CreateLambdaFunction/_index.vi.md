---
title : "Tạo hàm Lambda"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

1. Truy cập vào [giao diện quản trị của dịch vụ Lambda](https://console.aws.amazon.com/lambda/home).
  + Click chọn **Create function**.
  + Click **Author from scratch**.
  + Điền **Function name**.
  + Chọn Runtime **Python 3.9**.

![Connect](/images/3.connect/001-lambdafunc.png)

2. Tiếp đó.
  + Click chọn **Change default execution role**.
  + Click **Use an existing role**.
  + Chọn role đã tạo 

3. Sau khi tạo function xong copy code python vào tab **Code**
![Connect](/images/3.connect/002-lambdafunc.png)  


{{% notice note %}}
 Lặp lại các bước trên để tạo 1 function start EC2
 {{% /notice %}}

