EC2 Web Server + CloudWatch Monitoring (Project 4)

This project walks through deploying a simple Apache web server on an Amazon Linux EC2 instance, serving a custom webpage, and setting up CloudWatch monitoring with SNS email alerts.
It reflects real cloud support tasks: launching instances, configuring servers, enabling networking, and diagnosing issues through metrics and alerts.

What I Built

A working EC2 instance in us-east-2 (Ohio)

Installed and configured Apache (httpd)

Served a custom HTML page on port 80

Set inbound rules for HTTP access

Added CloudWatch + SNS monitoring to alert me when CPU gets high

Verified alarm trigger + recovery

This project demonstrates real AWS operational skills: Linux commands, networking, monitoring, and debugging.

Technologies Used

Amazon EC2

Amazon Linux 2023

Apache Web Server (httpd)

Security Groups

SSH

CloudWatch Alarms

SNS Notifications

Steps
1. Launch EC2 Instance

AMI: Amazon Linux 2023

Instance type: t2.micro (Free Tier)

Key pair: kd-ec2-keypair

Security group allowing SSH (22) and HTTP (80)

📸 Screenshots

2. Connect via SSH

Used my key pair to connect from macOS Terminal:

ssh -i ~/.ssh/kd-ec2-keypair.pem ec2-user@<Public-IP>

📸 Screenshot

3. Install Apache

Updated the instance and installed + enabled Apache:

sudo dnf update -y
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

📸 Screenshot

4. Allow HTTP in Security Group

Inbound rule added:

Type	Port	Source
HTTP	80	0.0.0.0/0
📸 Screenshot

5. Serve Custom Webpage

Replaced the default Apache page with my own:

echo "<h1>Hello from KD's EC2 Web Server 🎉</h1>" | sudo tee /var/www/html/index.html


Visited the Public IP to verify.

📸 Screenshot

Monitoring Extension (CloudWatch + SNS)
6. SNS Topic for Alerts

Created a topic called kd-ec2-alerts and subscribed my email.

📸 Screenshots




7. Create CloudWatch Alarm

Configured alarm:

Metric: CPUUtilization

Threshold: > 60%

Notification: kd-ec2-alerts SNS topic

📸 Screenshot

8. Trigger Alarm

Installed stress and simulated high CPU:

sudo yum install stress -y
stress --cpu 2


Alarm entered ALARM (red) and I received an SNS email.

📸 Screenshot

Cleanup

To avoid charges:

Stop/terminate EC2 instance

Delete CloudWatch alarm

Delete SNS topic (optional)
