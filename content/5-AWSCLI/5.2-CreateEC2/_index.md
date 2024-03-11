---
title : "Create Linux EC2"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---

### Introduce 

To create the EC2 instance in the AWS CLI with the minimum recommended set of parameters, use the following commands:


    aws ec2 run-instances \
        --image-id <ami-id> \
        --count 1 \
        --instance-type <instance-type> \
        --key-name <keypair-name> \
        --security-groups <security-group-name> \
        --subnet-id <subnet-id> \
        --associate-public-ip-address \
        --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=<name>}]' \
        --block-device-mappings '[{"DeviceName":"/dev/xvda","Ebs":{"VolumeSize":20,"VolumeType":"gp2"}}]'


To create an EC2 instance, we need to do: 

1. Select **AMI ID**: is the Image we want to use. In this case, we use the Amazon Linux 2 AMI (HVM) image with ID `ami-07761f3ae34c4478d`
2. Select Instance Type: In this case, we choose `t2.micro`
3. Generate Key-Pair: Create a key pair to use, which we name `ec2`
4. Create a Security Group: allow inbound traffic to SSH, HTTP or HTTPS ports. We name it `my-ec2-sg`
5. Select subnet: in this case we choose the default
6. Associate Public IP:  In this lab, you don't need to turn it on
7. Name for instance:  default
8. Configure storage: default
9. Launch


{{% notice info %}}
In this lab, I only install 2 EC2 by default for the lab, so I will only need to get the instance ID information
{{% /notice %}}

1. Chọn AMI ID:

   If you want detailed information about the AMI ID of the Amazon Linux 2 AMI image in the us-east-1 region, you can get the information when creating an instance using the interface.

    ![AMIID](/images/5.fwd/005-fwd.png)

    We will use this AMI ID to create an EC2 Instance. We have the value AMI_ID

    ```
    AMI_ID=ami-07761f3ae34c4478d
    ```

2. Select Instance Type:

    We use `t2.micro` as the Instance type.

    ```
        INSTANCE_TYPE=t2.micro
    ```

3. Create Key-Pair

    3.1. Generate a key pair to use. We name it `ec2` .
    
    ```
    aws ec2 create-key-pair \
        --key-name ec2  \
        --query 'KeyMaterial' \
        --output text > ec2.pem
    ```
    
    We will have a key-pair file named `ec2.pem` created in the path
    
   3.2. Next we need to grant permissions to the file if we want to ssh into ec2 (ignored in this lab).
    
    ```
    chmod 400 ec2.pem
    ```
    

4. Launch

    ```
    aws ec2 run-instances \
        --image-id ami-07761f3ae34c4478d \
        --count 2 \
        --instance-type t2.micro \
        --key-name ec2 \
        --query 'Instances[*].InstanceId'
    ```

    We will have output which is the instance ID of the 2 newly created Instances

