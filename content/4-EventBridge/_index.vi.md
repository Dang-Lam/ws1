---
title : "Tạo rule eventBridge schedules để chạy function theo lịch"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---


1. Mở EventBridge
  + Hãy click biểu tượng sao để được bookmark cho tiện sử dụng nhé
  
![LambdaFunction](/images/4.EventBridge/001-eventbridge.png)

2. Chọn EventBride 
  + Click **Create rule**

![CreateRule](/images/4.EventBridge/002-eventbridge.png)

3. Điền tên cho rule của bạn, ví dụ như **StopEC2Instance**
4. Với **Rule type**, chọn **Schedule**, sau đó chọn **Continue in EventBridge Scheduler**
![RuleType](/images/4.EventBridge/004-eventbridge.png)
5. Với **Schedule pattern,** chọn **Recurring schedule**
6. Với **Schedule type,** chọn một schedule type, sau đó hoàn thành các bước sau:
  + Với **Rate-based schedule,** một lịch trình chạy theo chu kỳ đều đặn, ví dụ mỗi 10 phút
  + Với **Cron-based schedule,** một lịch trình được đặt bằng biểu thức cron, chạy vào một thời điểm cụ thể, chẳng hạn như 8:00 sáng vào thứ 2 đầu tiên của mỗi tháng
  {{% notice note %}}
  Cron expressions được đánh giá theo giờ UTC. Nhớ chọn Time zone theo múi giờ +7
  {{% /notice %}}
![ScheduleType](/images/4.EventBridge/006-eventbridge.png)
7. Phần **Select targets** → **All APIs** → **AWS Lambda** → **invoke**
![Target](/images/4.EventBridge/007-eventbridge.png)
8. Chọn **next** → **Create Schedule**
![Schedule](/images/4.EventBridge/008-eventbridge.png)
9.  Lặp lại các bước từ 1-9 để tạo rule bật ec2instance.     
  + Khi hoàn thành xong các bước này thì EC2 của bạn đã sẵn sàng để chạy theo lịch