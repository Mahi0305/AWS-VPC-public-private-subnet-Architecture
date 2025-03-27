
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
![Screenshot 2025-03-27 144600](https://github.com/user-attachments/assets/35cef0e9-ec1f-4610-a9cf-955514182d4a)

### **Step 2: Configure Auto Scaling Group**
1. Create a **Launch Template** for EC2 instances
   ![Screenshot 2025-03-27 145527](https://github.com/user-attachments/assets/e7259b46-ce61-4024-8d7c-79a0930edcaa)
   ![Screenshot 2025-03-27 165040](https://github.com/user-attachments/assets/30bf6a98-1795-4194-9044-c6d69768e808)
   ![Screenshot 2025-03-27 145720](https://github.com/user-attachments/assets/1f366ca3-5e28-461a-b30a-f8ca1d676ade)
   ![Screenshot 2025-03-27 150202](https://github.com/user-attachments/assets/1bf60da6-60fc-4c74-9b76-4b4406b7e1cf)
On **Launch Template** we need to select Ubuntu **AMI**
2. Set up **Auto Scaling Policies**  
![Screenshot 2025-03-27 150356](https://github.com/user-attachments/assets/5eceb676-bf2b-42fe-af9b-6f071ea62064)
![Screenshot 2025-03-27 150527](https://github.com/user-attachments/assets/a64653f3-0d7f-464e-865e-1d374030adf4)
![Screenshot 2025-03-27 150725](https://github.com/user-attachments/assets/adb1a730-9b7a-4fbf-b233-1202ecc9ccb0)
![Screenshot 2025-03-27 150812](https://github.com/user-attachments/assets/a3310ece-99a2-4993-bcf8-cd2353a27ab9)
![Screenshot 2025-03-27 151206](https://github.com/user-attachments/assets/73c79b9d-5612-4015-8e6a-0ff23999c284)

3. Now your are Successfully Created Auto Scaling Group.
4. Open the AWS Management Console.
5. Navigate to the EC2 console by clicking on "Services" in the top-left corner, then selecting "EC2" under the "Compute" section.
6. In the EC2 dashboard, you'll find the "Instances" link on the left-hand navigation pane. Click on "Instances."
7. Here, you should see the list of EC2 instances associated with your account. Look for the instances created by your Auto Scaling Group.
Since you mentioned that the Auto Scaling Group launched instances in different AZs, you can check the "Availability Zone" column to verify that these instances are indeed distributed across multiple AZs.

### **Step 3: Deploy a Bastion Host**
1. Create an EC2 instance in the **public subnet**
2. Creating the **Bastion Host** :
   ![Screenshot 2025-03-27 151400](https://github.com/user-attachments/assets/af145e46-65c1-496b-a88c-109a3b4eff1e)
   ![Screenshot 2025-03-27 151457](https://github.com/user-attachments/assets/7f9da77d-8bb1-451b-a91c-ff0c8d3b9a0c)
   ![Screenshot 2025-03-27 151644](https://github.com/user-attachments/assets/bee054a2-89a7-4108-bf21-0edf52dfd170)

## **🔧 How to SSH into Private Instances**
SSH into the Bastion Host Instance: To SSH into the private instances, we first need to connect to our Bastion host instance. From there, we'll be able to SSH into the private instance.

Ensure the PEM File is Present on the Bastion Host: Additionally, make sure that the PEM file is present on the Bastion host. Without it, you won't be able to SSH into the private instance from the Bastion host.

Open a Terminal: Open a terminal window on your local machine.

# Execute the Following Commands:

a. If your PEM file is named something like <prod.pem>, you must remove spaces in the filename.

b. Copy the PEM file to the Bastion host using the scp command. Replace <pem file location> with the local and remote file paths, and <bastion host public IP> with the Bastion host's public IP address. Example:

scp -i C:\Users\capta\Downloads\prod.pem C:\Users\capta\Downloads\prod.pemubuntu@34.229.240.123:/home/ubuntu

# Connect to Bastion Host
ssh -i prod.pem ubuntu@<Bastion_Public_IP>
chmod 400 prod.pem

# Connect to Private Instance from Bastion
ssh -i prod.pem ubuntu@<Private_Instance_IP>

# We will deploy our application on one of the private instances to test the load balancer.
curl -L -o wedding-lite.zip " https://www.tooplate.com/view/2131-wedding-lite"

# Finally, start a Python HTTP server on port 8000 to deploy your application on the private instance:
python3 -m http.server 8000

# Note :
We intentionally deployed the application on only one instance to check if the Load Balancer will distribute 50% of the traffic to one instance (which will receive a response) and 50% to another instance (which will not receive a response).

### **Step 4: Creating the Load Balancer**

 # create a target group.
 ![Screenshot 2025-03-27 160358](https://github.com/user-attachments/assets/1b448ed0-92bb-4bf2-b6b5-ec26a6eac541)
 ![Screenshot 2025-03-27 160426](https://github.com/user-attachments/assets/aa8c9b49-b0a2-418a-9221-4d2e487bbcbe)
 ![Screenshot 2025-03-27 160450](https://github.com/user-attachments/assets/237af22f-ca10-444e-be1c-d2378fd48efe)

 # create a Application Load Balancer.
![Screenshot 2025-03-27 160559](https://github.com/user-attachments/assets/80111860-618d-40ee-b1d3-4a7e8aefce38)
![Screenshot 2025-03-27 160613](https://github.com/user-attachments/assets/6a4def28-97fc-4cc2-a19e-a08aadcf4d38)
![Screenshot 2025-03-27 160628](https://github.com/user-attachments/assets/81a5fc48-5cd5-4acf-a5d2-a5b708737d9e)
![Screenshot 2025-03-27 160836](https://github.com/user-attachments/assets/e8b974e3-feaf-4393-8b64-c8ec7ad61511)








