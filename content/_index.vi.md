---
title : "Tối ưu chi phí với Lambda"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Tối ưu chi phí với Lambda

### Tổng quan

 Trong bài lab này, chúng ta sẽ khởi tạo EC2, tìm hiểu về Lambda và thực hành tự động dừng và khởi động các phiên bản EC2 của mình để giảm mức sử dụng Amazon EC2 theo lịch bằng EventBridge

![ConnectPrivate](/images/arc-log.png) 

### Nội dung

 1. [Giới thiệu](1-introduce/)
 2. [Các bước chuẩn bị](2-Prerequiste/)
 3. [Tạo Lambda function để start/stop EC2 Instances](3-LambdaFunction/)
 4. [Tạo rule eventBridge schedules để chạy function theo lịch](4-EventBridge/)
 5. [Mở rộng với AWS CLI](5-AWSCLI/)
 6. [Dọn dẹp tài nguyên](6-cleanup/)
