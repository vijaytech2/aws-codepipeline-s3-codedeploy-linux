# aws-codepipeline-s3-aws-codedeploy_linux
Use this sample when creating a simple pipeline in AWS CodePipeline while following the Simple Pipeline Walkthrough tutorial. http://docs.aws.amazon.com/codepipeline/latest/userguide/getting-started-w.html
# here is the user data for installing aws code deploy agent on ec2instance
#!/bin/bash -x
REGION=$(curl 169.254.169.254/latest/meta-data/placement/availability-zone/ sed 's/[a-z]$//)
yum update -y
yum install ruby wget -y
yum install httpd
cd /home/ec2-user 
wget https://aws-codedeploy-$REGION.s3.amazonaws.com/latest/install
chmod +x ./install
./install auto

# IAM Roles
Create following IAM roles and attach the policies
1. IAM role for Instance profile
2. IAM role for Service profile

Role-1: Instance Role - CodeDeployInstanceRole
Attach follwing policies
a. AmazonEC2RoleforAWSCodeDeploy - This allow EC2 instance under CodeDeploy to access S3
b. AutoScalingNotificationAccessRole - This allow EC2 instance under CodeDeploy to access SNS and SQS

Role-2: Service Role - CodeDeployServiceRole

Attach following policies:
a. AWSCodeDeploeRole - This allows the CodeDeploy service to access autoscaling/ec2/sns

Note: Edit Trust Relationship to ensure - "service":"codedeploy.amazonaws.com" 
