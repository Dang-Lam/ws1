---
title : "Introduce AMS CLI"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

### Introduce 

By using the AWS CLI, we can deploy more quickly and securely than using the GUI. In this article we will create all the steps using AWS CLI



![port-fwd](/images/arc-log.png) 






### Content

 1. [Create Role](5.1-CreateRole/)
 2. [Create EC2](5.2-CreateEC2/)
 3. [Create Lambda function to start/stop EC2 Instances](5.3-LambdaFunction/)
 4. [Create rule eventBridge schedules to run function](5.4-EventBridgeSchedule/)