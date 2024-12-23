# AWS VPC Peering

## 🌍 Overview
This project demonstrates how to implement VPC Peering using Amazon Web Services (AWS). The goal is to create a secure and efficient connection between two VPCs for seamless communication without traversing the public internet.

## 🏗️ Architecture
<img src="Architecture%20Diagram.png" alt="VPC Peering Architecture Diagram" width="500"/>

## 🥳 Prerequisites
- AWS Account
- IAM user with sufficient permissions
- Elastic IP allocation knowledge
- Familiarity with AWS Management Console

## 🛠️ Setup Instructions

### Step 1: Set Up VPCs
1. Use the AWS VPC Launch Wizard to deploy two VPCs.
2. Assign unique CIDR blocks:
   - VPC 1: `10.1.0.0/16`
   - VPC 2: `10.2.0.0/16`
3. Create one public subnet in each VPC.

### Step 2: Create a VPC Peering Connection
1. Navigate to the VPC Dashboard in AWS.
2. Select "Create Peering Connection."
3. Specify the **Requester** and **Accepter** VPCs.
4. Accept the peering connection request.

### Step 3: Update Route Tables
1. Navigate to the Route Tables section in the VPC Dashboard.
2. Add a route in each VPC's route table with:
   - Destination: The CIDR block of the other VPC.
   - Target: The created VPC Peering Connection.

### Step 4: Launch EC2 Instances
1. Launch an EC2 instance in the public subnet of each VPC.
2. Ensure both instances have security groups configured to allow necessary traffic.

### Step 5: Test Connectivity
1. Use **EC2 Instance Connect** to access the first EC2 instance.
2. From EC2 Instance 1, ping the private IPv4 address of EC2 Instance 2 to validate the peering connection.

## 📝 Configuration Details

### VPC Configuration
- **VPC 1 CIDR Block:** `10.1.0.0/16`
- **VPC 2 CIDR Block:** `10.2.0.0/16`

### Security Group Configuration
- Allow **ICMP traffic** for ping tests between the two VPCs.

### Elastic IPs
- Elastic IPs were associated with EC2 instances for public IPv4 address allocation.

## 🍴 Usage Instructions
1. SSH into EC2 Instance 1 using Instance Connect or an Elastic IP.
2. Run the `ping` command to test the connection with the second instance:
ping <private-ip-of-instance-2>

markdown
Copy code
3. Verify successful connectivity.

## 🚨 Troubleshooting

### Common Issues
- **Unable to connect to an EC2 instance:**
- Ensure the instance has a public IPv4 address (Elastic IP) and is in a public subnet.
- **Ping test fails:**
- Verify the security group rules allow inbound ICMP traffic from the other VPC.

### Elastic IP Setup
1. Allocate an Elastic IP from the AWS console.
2. Associate it with the EC2 instance in the public subnet.

## 📚 Additional Resources
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [AWS Elastic IP Documentation](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses.html)
