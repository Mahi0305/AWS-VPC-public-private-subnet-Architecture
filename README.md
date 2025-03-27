# AWS-VPC-public-private-subnet-Architecture
Secure VPC Architecture with Public and Private Subnets for Production Environment
Overview :
This project's overview is depicted in the diagram below. The setup revolves around a Virtual Private Cloud (VPC) featuring both public and private subnets, thoughtfully distributed across two Availability Zones to ensure reliability.

Within each public subnet, there's a NAT gateway to facilitate outbound internet connectivity and a load balancer node for effective traffic distribution.

On the other hand, the project's servers reside in the private subnets. Their deployment and termination are automated through an Auto Scaling group, allowing them to dynamically adapt to workload changes. These servers play a pivotal role in receiving traffic from the load balancer and can access the internet through the NAT gateway when necessary![Screenshot 2025-02-25 001529](https://github.com/user-attachments/assets/e0d08182-af38-47c7-8298-3a17981e8b9f)

Steps :
Step 1 :
Create the VPC :
1.Open the Amazon VPC console by visiting https://console.aws.amazon.com/vpc/.

2.On the dashboard, click on "Create VPC."

3.Under "Resources to create," select "VPC and more."

4.Configure the VPC:

a. Provide a name for the VPC in the "Name tag auto-generation" field.

b. For the IPv4 CIDR block, leave it as default suggestion.

5.Configure the subnets:

a. Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.

b. Specify the "Number of public subnets" as 2.

c. Specify the "Number of private subnets" as 2.

d. For NAT gateways, choose "1 per AZ" to enhance resiliency.

g. For VPC endpoints, you can choose "None" .

h. Regarding DNS options, clear the checkbox for "Enable DNS hostnames."

Once you've configured all the settings, click "Create VPC."
