---
title : "Tạo Linux EC2"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5.2 </b> "
---

### Giới thiệu 

Cấu trúc để tạo một EC2 Instance sử dụng AWS CLI như sau:


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


Để tạo một EC2 instance, chúng ta cần làm: 

1. Chọn **AMI ID**: là một Image chúng ta muốn sử dụng. Trong case này, chúng ta sử dụng image Amazon Linux 2 AMI (HVM) có ID là `ami-07761f3ae34c4478d`
2. Chọn Instance Type: Trong case này, ta chọn `t2.micro`
3. Tạo Key-Pair: Tạo một cặp khóa để sử dụng, chúng ta đặt tên là `ec2`
4. Tạo một Security Group: cho phép inbound traffic đến port SSH, HTTP hay HTTPS. Ta đặt tên là my-ec2-sg
5. Chọn subnet: trong trường hợp này ta chọn mặc định 
6. Associate Public IP:  trong bài lab này không cần bật cũng được
7. Name cho instance:  ta để theo mặc định 
8. Cấu hình storage: ta đặt theo mặc định
9. Khởi chạy


{{% notice info %}}
Trong lab này mình chỉ cài 2 EC2 theo mặc định để lab nên sẽ chỉ cần lấy thông tin instance ID
{{% /notice %}}

1. Chọn AMI ID:

    Muốn có thông tin chi tiết AMI ID của image Amazon Linux 2 AMI trong region us-east-1, ta có thể lấy thông tin khi tạo instance bằng giao diện

![AMIID](/images/5.fwd/005-fwd.png)

Ta sẽ sử dụng AMI ID này để tạo EC2 Instance. Ta có giá trị AMI_ID

    ```
    AMI_ID=ami-07761f3ae34c4478d
    ```

2. Chọn Instance Type:

Ta sử dụng `t2.micro` là kiểu Instance. 

    ```
        INSTANCE_TYPE=t2.micro
    ```

3. Tạo Key-Pair

4. Tạo một cặp khóa để sử dụng. Ta đặt tên là `ec2` .
    
    ```
    aws ec2 create-key-pair \
        --key-name ec2  \
        --query 'KeyMaterial' \
        --output text > ec2.pem
    ```
    
    Ta sẽ có file key-pair tên là `ec2.pem` được tạo trong đường dẫn 
    
5. Tiếp theo ta cần cấp quyền cho file nếu muốn ssh vào ec2 (trong bài lab này bỏ qua)
    
    ```
    chmod 400 ec2.pem
    ```
    

6. Khởi chạy

    ```
    aws ec2 run-instances \
        --image-id ami-07761f3ae34c4478d \
        --count 2 \
        --instance-type t2.micro \
        --key-name ec2 \
        --query 'Instances[*].InstanceId'
    ```

    Chúng ta sẽ có output là instance ID của 2 Instance vừa tạo

    ```
    [
        "i-0c899a57eb77e26a0",
        "i-072bcd2e760962f7f"
    ]

    ```



