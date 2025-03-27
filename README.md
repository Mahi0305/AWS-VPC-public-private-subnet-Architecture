# AWS-VPC-public-private-subnet-Architecture
Secure VPC Architecture with Public and Private Subnets for Production Environment
Overview :
This project's overview is depicted in the diagram below. The setup revolves around a Virtual Private Cloud (VPC) featuring both public and private subnets, thoughtfully distributed across two Availability Zones to ensure reliability.
Within each public subnet, there's a NAT gateway to facilitate outbound internet connectivity and a load balancer node for effective traffic distribution.On the other hand, the project's servers reside in the private subnets. Their deployment and termination are automated through an Auto Scaling group, allowing them to dynamically adapt to workload changes. These servers play a pivotal role in receiving traffic from the load balancer and can access the internet through the NAT gateway when necessary![Screenshot 2025-02-25 001529](https://github.com/user-attachments/assets/e0d08182-af38-47c7-8298-3a17981e8b9f)

