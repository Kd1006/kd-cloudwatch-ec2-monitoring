# kd-cloudwatch-ec2-monitoring
EC2 + Cloudwatch + SNS monitoring project : Create alarms, trigger CPU spike and receive email alerts.  

This project demonstrates how to set up basic monitoring on an Amazon EC2 instance using Amazon CloudWatch, SNS notifications, and a simple CPU-load simulation.
The goal is to show how an engineer can create operational visibility and receive automated alerts when an instance becomes unhealthy or overloaded.

## What the Project Covers

Launching an EC2 instance (Amazon Linux 2023)

Installing and configuring Apache HTTP Server

Serving a test webpage from the instance

Creating a CloudWatch alarm to monitor CPU utilization

Setting up an SNS topic + email subscription for alerts

Triggering the alarm manually by generating high CPU load

Observing alarm state changes (OK → ALARM → OK)

This is a practical, hands-on workflow often used in cloud operations and DevOps roles.

---

## EC2 Instance Setup

OS: Amazon Linux 2023

Web server: Apache (httpd)

Created a simple HTML file at /var/www/html/index.html:

<h1>Hello from KD’s EC2 Web Server 🎉</h1>
<p>This page is served from an Amazon Linux EC2 instance in us-east-2.</p>


This allowed verifying that the instance was publicly reachable and serving traffic correctly.

## CloudWatch Alarm

I created a CloudWatch alarm to monitor CPUUtilization for the EC2 instance.

Alarm settings:

Metric: CPUUtilization

Threshold: > 60%

Period: 5 minutes

Whenever the value is Greater than the threshold

When the alarm enters ALARM state, it triggers an SNS notification.

--- 

### SNS Setup

Created an SNS Topic:

Name: kd-ec2-alerts
Subscription: My email address
Once confirmed, the alarm successfully delivered alert messages when CPU spiked.

--- 

### Triggering the Alarm

To test the alarm, I intentionally generated high CPU load:
```bash
yes > /dev/null &
```

This pushed CPU usage above the threshold and caused the alarm to enter ALARM state.
After terminating the process:
```bash 
killall yes
```

CPU returned to normal and the alarm moved back to OK state.

## Screenshots Included

The repository contains the following:
![EC2 instance created](screenshots/01-ec2-instance-created.png)

02-sns-topic-created.png

03-sns-email-confirmation.png

04-cloudwatch-alarm-created.png

05-cloudwatch-alarm-in-alarm-state.png

06-email-alert-received.png

07-alarm-history-recovery.png

These demonstrate the setup, the alarm firing, and the recovery process.

## What This Project Shows

### This project highlights:

Basic AWS monitoring principles

How to integrate CloudWatch + SNS for automated alerting

How to validate monitoring using CPU load tests

Cloud engineering fundamentals used in real production systems

It’s a great foundational example of operational visibility in AWS.
