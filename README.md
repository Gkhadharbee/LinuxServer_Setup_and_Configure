# Linux Server Setup and Configuration

## Introduction

This project provides a comprehensive guide to setting up and configuring a Linux server. The goal is to ensure a secure, optimized, and well-maintained environment for hosting applications or services.

## Prerequisites

Before you begin, ensure you have the following:

- A fresh Linux server installation (Ubuntu, Debian, CentOS or Amazon Linux)

- SSH access to the server

- Basic knowledge of Linux command-line operations

## Installation and Setup Steps

### <p align="">Step1:Launch an AWS EC2 Instance</p>>

1. Log in to AWS Management Console.

2. Navigate to EC2 service and click Launch Instance.

3. Choose any AMI(Linux Server). Here, I used Amazon Linux AMI.

4. Select an instance type (e.g., t2.micro for free tier eligibility).

5. Configure instance details and security groups.

6. Add storage as needed.

7. Launch the instance and download the key pair (.pem file).

### <p align="">Step2:Connect to the EC2 Instance via SSH</p>
- Connect to the instance via SSH

```bash
ssh -i /path/to/your-key.pem ec2-user@your-instance-public-ip
```

- Update the System

```
sudo yum update -y
```

### <p align="">Step3:Create a New User</p>
- To create a new user with sudo privileges to avoid working as the root user:
```bash
sudo adduser newuser
sudo usermod -aG wheel newuser  # Grant sudo privileges
```

### <p align="">Step4:Configure SSH Access</p>
- To configure ssh access

```bash
sudo nano /etc/ssh/sshd_config
```

- Modify the following lines:

```bash
PermitRootLogin no
PasswordAuthentication no
```

- Restart SSH service:

```bash
sudo systemctl restart sshd
```

### <p align="">Step5:Setup AWS Security Groups</p>

- Navigate to the EC2 Dashboard.

- Select your instance and open the Security Groups settings.

- Allow necessary ports (e.g., SSH - 22, HTTP - 80, HTTPS - 443).

### <p align="">Step6:Install Essential Packages</p>
- To Install Essential Packages

```bash
sudo yum install -y curl wget git unzip
```

### <p align="">Step7:Configure a Web Server(Apache)</p>
- To Configure a Web Server(Apache)

```bash
sudo yum install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd
```

### <p align="">Step9:Secure the Server</p>

- Use SSH keys for authentication.

- Enable automatic security updates.

- Configure fail2ban to prevent brute-force attacks.

```bash
sudo amazon-linux-extras enable epel
sudo yum install -y fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### <p align="">Step10:Monitor Server Performance</p>

- top
- htop  # Install with 'sudo yum install htop'

## Conclusion

Successfully setup and configured the Linux Server.

