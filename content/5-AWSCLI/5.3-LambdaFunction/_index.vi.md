---
title : "Mở rộng với AWS CLI"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

### Giới thiệu 

Với việc sử dụng AWS CLI, chúng ta có thể triển khai một cách nhanh chóng và an toàn hơn so với việc sử dụng GUI. Trong bài này chúng ta sẽ tạo tất cả các bước bằng AWS CLI nhé



![port-fwd](/images/arc-log.png) 






### Nội dung

 1. [Tạo Role](5.1-CreateRole/)
 2. [Tạo EC2](5.2-CreateEC2/)
 3. [Tạo Lambda function để start/stop EC2 Instances](5.3-LambdaFunction/)
 4. [Tạo rule eventBridge schedules để chạy function theo lịch](5.4-EventBridgeSchedule/)