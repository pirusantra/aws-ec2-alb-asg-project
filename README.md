# Project 1: Scalable Web Application with ALB and Auto Scaling

This project serves a static web page from Amazon EC2 instances. The infrastructure is designed to be resilient and to handle varying levels of traffic by automatically adjusting the number of instances based on demand.

# Technologies Used
HTML: The front-end of the application.

AWS EC2: Virtual servers running the application.

AWS Application Load Balancer (ALB): Distributes incoming web traffic across multiple EC2 instances.

AWS Auto Scaling Group (ASG): Automatically scales the number of EC2 instances in response to traffic demand and health checks.

AWS Route 53: A scalable cloud DNS service that routes user requests to the ALB.

AWS CloudWatch: A monitoring service that collects metrics used by the ASG for scaling decisions

## ⚙️ Deployment Steps
### 1️⃣ EC2 Setup
- Launched an **Amazon Linux 2** instance (`t2.micro` – Free Tier).
- Created and downloaded a key pair (`WebKey.pem`) for SSH access.
- Configured a **Security Group** to allow:
  - **SSH (22)** only from my IP
  - **HTTP (80)** from anywhere

### 2️⃣ Connecting & Installing Apache
- Connected to EC2 via SSH using the key pair.
- Installed and started the **Apache web server (httpd)**.
- Enabled the service so it runs on every reboot.

### 3️⃣ Deploying the Web Page
- Created an `index.html` file inside `/var/www/html`.
- Added a simple HTML page for the application.
- Verified that the webpage loaded successfully in the browser using the EC2 public IP.

### 4️⃣ Creating an AMI
- Created an **Amazon Machine Image (AMI)** of the configured instance.
- This AMI was later used in the Auto Scaling Group to ensure new instances had the same configuration.

### 5️⃣ Auto Scaling Group (ASG)
- Created a **Launch Template** using the AMI.
- Configured an **Auto Scaling Group** with:
  - Minimum capacity = 1
  - Desired capacity = 2
  - Maximum capacity = 3
- Selected multiple availability zones for high availability.

### 6️⃣ Application Load Balancer (ALB)
- Configured an **Application Load Balancer** in front of the Auto Scaling Group.
- Created a **Target Group** and registered the ASG instances.
- Verified that the ALB distributed incoming traffic across multiple instances.

---

## 🌐 Final Output
- Webpage was accessible using the **ALB DNS name**.
- Traffic was automatically distributed across EC2 instances.
- When load increased, ASG automatically launched new instances.



