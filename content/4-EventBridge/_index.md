---
title : "Create rule eventBridge schedules to run Lambda function"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---


1. Open EventBridge
  + Click start icon to bookmark
  
![LambdaFunction](/images/4.EventBridge/001-eventbridge.png)

2. Click EventBride 
  + Click **Create rule**

![CreateRule](/images/4.EventBridge/002-eventbridge.png)

3. Fill name your rule, example **StopEC2Instance**
4. In **Rule type**, Choose **Schedule**, then choose **Continue in EventBridge Scheduler**
![RuleType](/images/4.EventBridge/004-eventbridge.png) 
5. In **Schedule pattern,** choose **Recurring schedule**
6. In **Schedule type,** choose schedule type, then complete the following steps:
  + In **Rate-based schedule,** a schedule that runs at regular intervals, for example every 10 minutes
  + In **Cron-based schedule,** a schedule set using a cron expression, to run at a specific time, such as 8:00 a.m. on the first Monday of each month
  {{% notice note %}}
  Cron expressions are evaluated in UTC time.
  {{% /notice %}}
![ScheduleType](/images/4.EventBridge/006-eventbridge.png)
7. in **Select targets** → **All APIs** → **AWS Lambda** → **invoke**
![Target](/images/4.EventBridge/007-eventbridge.png)
8. In **next** → **Create Schedule**
![Schedule](/images/4.EventBridge/008-eventbridge.png)
9. Repeat steps 1-9 to create a rule to enable ec2instance.
  + Once you have completed these steps, your EC2 is ready to run on schedule