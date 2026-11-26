# AWS Expense Tracker Deployment on Amazon EC2

A hands-on AWS Cloud project demonstrating how to deploy a static Expense Tracker web application on an Amazon EC2 instance running **Amazon Linux 2023** with **Apache HTTP Server (httpd)**.

This project focuses on cloud hosting fundamentals, Linux server administration, web server configuration, and network access control.

## Project Overview

The Expense Tracker frontend is built using:

- **HTML** – Page structure
- **CSS** – Styling and layout
- **JavaScript** – Client-side interactions

The application is hosted on an EC2 virtual server and served through Apache HTTP Server over HTTP.

## Architecture

```text
User's Browser
      |
      | HTTP (Port 80)
      v
AWS EC2 Instance
Amazon Linux 2023
      |
      v
Apache HTTP Server
      |
      v
Expense Tracker
HTML / CSS / JavaScript
```

## AWS Services and Technologies

| Service / Technology | Purpose |
|---|---|
| Amazon EC2 | Virtual server hosting the website |
| Amazon Linux 2023 | Linux operating system |
| Apache HTTP Server | Serves the web application |
| AWS Security Groups | Controls network traffic |
| HTML, CSS, JavaScript | Frontend development |

## Key Technical Learnings

- Launching and accessing an AWS EC2 instance
- Linux server administration
- Installing and managing Apache HTTP Server
- Deploying static website files on a cloud server
- Configuring HTTP access through Security Groups
- Troubleshooting website connectivity and deployment issues

## Deployment Steps

### 1. Launch an EC2 Instance

1. Open the AWS Management Console.
2. Navigate to Amazon EC2.
3. Launch an instance using Amazon Linux 2023.
4. Select an instance type suitable for your workload.
5. Configure secure access using a key pair or another supported method.

### 2. Configure Security Groups

Configure the following inbound rules:

| Type | Port | Source |
|---|---:|---|
| SSH | 22 | Your trusted IP address |
| HTTP | 80 | `0.0.0.0/0` |

**Security note:** Avoid exposing SSH access to the entire internet. Restrict administrative access to trusted IP addresses or use AWS Systems Manager Session Manager where appropriate.

### 3. Install Apache HTTP Server

Connect to your EC2 instance and run:

```bash
sudo dnf update -y
sudo dnf install -y httpd
sudo systemctl enable --now httpd
```

Verify the Apache service:

```bash
sudo systemctl status httpd
```

### 4. Deploy Website Files

Copy the Expense Tracker application files to Apache's document root:

```bash
sudo cp -r /path/to/expense-tracker/* /var/www/html/
```

Replace `/path/to/expense-tracker/` with your actual application directory.

Ensure the main page is named:

```text
index.html
```

### 5. Verify the Deployment

Open your browser and visit:

```text
http://<EC2-PUBLIC-IP>
```

Check the following if the website does not load:

- EC2 instance is running
- Apache service is active
- Security Group allows HTTP traffic on port 80
- Website files exist in `/var/www/html/`
- Instance has the required network connectivity

Apache error logs can be checked using:

```bash
sudo tail -n 50 /var/log/httpd/error_log
```

## Security Considerations

This project demonstrates a basic HTTP deployment and is intended for learning.

Before using a similar setup in production:

- Configure HTTPS and redirect HTTP to HTTPS
- Follow the principle of least privilege for IAM permissions
- Restrict administrative access
- Keep the operating system and web server updated
- Never store AWS credentials or secrets in frontend files
- Review Security Group rules regularly
- Implement monitoring and backup strategies

## Future Improvements

These are planned learning goals and are not claimed as completed features.

- [ ] Configure HTTPS and SSL/TLS
- [ ] Integrate Amazon CloudFront for content delivery
- [ ] Configure a custom domain using Amazon Route 53
- [ ] Implement EC2 security hardening
- [ ] Configure Amazon CloudWatch monitoring and alarms
- [ ] Automate deployment using GitHub Actions CI/CD
- [ ] Practice EBS snapshots and recovery strategies

**Note:** AWS Certificate Manager certificates are commonly used with supported AWS services such as CloudFront or an Application Load Balancer. For direct HTTPS on an EC2 Apache server, an appropriate certificate installation and renewal approach is required.

## Learning Outcome

This project helped me gain practical experience with AWS cloud hosting, Linux server administration, Apache web server configuration, and network access control.

My next goal is to move beyond basic website hosting and explore how to build, secure, monitor, and maintain reliable cloud infrastructure.

I am continuously learning and building hands-on projects as an aspiring **AWS Cloud Engineer**.

Feedback and suggestions from Cloud and DevOps professionals are always welcome!

---

**Repository:** [Amazon-EC2-Deployment](https://github.com/syedibrahimdev20-bot/Amazon-EC2-Deployment)
