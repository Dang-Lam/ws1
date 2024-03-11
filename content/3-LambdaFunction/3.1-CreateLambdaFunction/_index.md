---
title : "Create Lambda Function"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---
1. Go to  [AWS Lambda console](https://console.aws.amazon.com/lambda/home).
  + Click choose **Create function**.
  + Click **Author from scratch**.
  + Fill **Function name**.
  + Click Runtime **Python 3.9**.

![Connect](/images/3.connect/001-connect.png)

2. Next then
  + Click choose **Change default execution role**.
  + Click **Use an existing role**.
  + Select the created role

3. After creating the function, copy the python code into the tab **Code**
![Connect](/images/3.connect/002-connect.png)  


{{% notice note %}}
 Repeat the above steps to create a function to start EC2
 {{% /notice %}}
