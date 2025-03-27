
# **AWS Secure VPC Architecture with Public & Private Subnets**  


## **📖 Overview**  
This project sets up a **secure VPC architecture** with **public and private subnets** across multiple **Availability Zones** in AWS. The infrastructure includes:  
- **NAT Gateways** for outbound internet access  
- **Application Load Balancer (ALB)** for traffic distribution  
- **Auto Scaling Group** for high availability  
- **Bastion Host** for secure SSH access  
- **EC2 Instances** running in private subnets  

---

## **📌 Architecture Diagram**  
![Screenshot 2025-03-27 113522](https://github.com/user-attachments/assets/3727bc29-1bc5-4817-a703-ca97ae9557ba)


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
1. Open the Amazon VPC console by visiting https://console.aws.amazon.com/vpc/.
2. On the dashboard, click on "Create VPC."
3. Under "Resources to create," select "VPC and more."
4. Configure the VPC:

   a. Provide a name for the VPC in the "Name tag auto-generation" field.
   
   b. For the IPv4 CIDR block, leave it as default suggestion.
5. Configure the subnets:

   a. Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.
   
   b. Specify the "Number of public subnets" as 2.
   
   c. Specify the "Number of private subnets" as 2.
   
   d. For NAT gateways, choose "1 per AZ" to enhance resiliency.
   
   g. For VPC endpoints, you can choose "None" .
   
   h. Regarding DNS options, clear the checkbox for "Enable DNS hostnames."
   
Once you've configured all the settings, click "Create VPC."
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
