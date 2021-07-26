# nodejs-express-on-aws-ec2

1. create source
1. provisioning: appspec.yml
1. create configuration scripts
1. create IAM for EC2
   1. create role
   1. ec2 use case
   1. next: permission
   1. search: codedeploy
   1. checkbox: AmazonEc2RoleforAWSCodeDeploy
   1. next:Tags
   1. next:Review
1. create IAM for CodeDeploy
   1. create role
   1. CodeDeploy use case
   1. next:Permission
   1. next:Tags
   1. next:Review
1. Create EC2
   1. Click instances
   1. Launch instances
   1. Linux
   1. t2.micro
   1. next: Configure Instance Details
   1. IAM Role/ EC2CodeDeploy
   1. Advance Details/User data/ system installation scripts
   ```bash
#!/bin/bash
sudo yum -y update
sudo yum -y install ruby
sudo yum -y install wget
cd /home/ec2-user
wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
sudo chmod +x ./install
sudo ./install auto
   ```
   1. Next:AddStorage
   1. Next:AddTags
   1. Click: Add Tag, Key=Name, Value=ExpressApp
   1. Next:Configure Security Group
      1. Open Port 80 for external
      1. Open Port 3000 for internal (ALB or API gateway)
   1. Review Launch
   1. Launch
   1. Create new key pair
   1. Download key pair
