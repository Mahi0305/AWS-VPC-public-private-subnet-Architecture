
# **AWS Secure VPC Architecture with Public & Private Subnets**  

![AWS VPC Architecture](image-link-here)

## **📖 Overview**  
This project sets up a **secure VPC architecture** with **public and private subnets** across multiple **Availability Zones** in AWS. The infrastructure includes:  
- **NAT Gateways** for outbound internet access  
- **Application Load Balancer (ALB)** for traffic distribution  
- **Auto Scaling Group** for high availability  
- **Bastion Host** for secure SSH access  
- **EC2 Instances** running in private subnets  

---

## **📌 Architecture Diagram**  
_(Add an architecture diagram if available)_

---

## **📦 Features**
- ✅ **High Availability:** Uses multiple Availability Zones (AZs)  
- ✅ **Security:** Instances in private subnets with restricted access  
- ✅ **Scalability:** Auto Scaling Group automatically adjusts instances  
- ✅ **Traffic Management:** Load Balancer distributes traffic efficiently  
- ✅ **Cost-Effective:** Uses NAT Gateway for internet access instead of public IPs  

---

## **🚀 Setup Instructions**  
### **Step 1: Create a VPC**
1. Go to the AWS VPC console → Create VPC  
2. Choose **2 Public Subnets & 2 Private Subnets**  
3. Set up **NAT Gateways & Route Tables**  

### **Step 2: Configure Auto Scaling Group**
1. Create a **Launch Template** for EC2 instances  
2. Set up **Auto Scaling Policies**  

### **Step 3: Deploy a Bastion Host**
1. Create an EC2 instance in the **public subnet**  
2. Enable SSH access from your IP  
3. Use it to connect to **private instances**  

### **Step 4: Configure Load Balancer**
1. Create an **Application Load Balancer**  
2. Attach it to the **Auto Scaling Group**  
3. Add **HTTPS (SSL) support**  

---

## **🔧 How to SSH into Private Instances**
```sh
# Connect to Bastion Host
ssh -i my-key.pem ubuntu@<Bastion_Public_IP>

# Connect to Private Instance from Bastion
ssh -i my-key.pem ubuntu@<Private_Instance_IP>
