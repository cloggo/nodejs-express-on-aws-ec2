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
1. create CodeDeploy
   1. search service deploy
   1. CodeDeploy
   1. Select Applications
   1. Create Application
      1. Application Name: express-app, Compute Platform: EC2/On-premises
   1. next: create application
   1. create deployment group
      * dployment group name: express-app-group
      * service role: CodeDeployRole
      * Deployment Type: In-place
      * Environment Configuration: Amazon EC2 Instances
        * tag group: key = Name, Value = ExpressApp
      * Load Balancing: Once instance so don't need
1. create PipeLine
   1. Choose PipeLine
   1. create pipeline
      * pipeline name: express-app-pipeline, default location
   1. next
   1. source, github 2
   1. first time: connect to github
   1. select repo and branch, output artifact format: default
   1. build stage: none for this project
   1. Add deploy stage: AWS CodeDeploy
      Application Name: express-app, Application Group: express-app-group
   1. verification
      details and then events
1. verify ec2 instances
   1. search ec2
   1. ec2
   1. instances
   1. check the instance created
   1. copy public IP4 DNS
   1. open new tab: ec2-3-136-155-212.us-east-2.compute.amazonaws.com:3000
