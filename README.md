# Setting-Up-a-Peering-Connection

### Challenge Overview:
Organizations often operate multiple Amazon Virtual Private Clouds (VPCs) to isolate and manage resources securely. However, a common challenge arises when communication is needed between these VPCs to share data or access services. The challenge was to establish secure, low-latency connectivity while maintaining network isolation and adhering to AWS best practices for routing and security.

### Objective:
1.	Establish Secure Connectivity: Create a secure VPC peering connection between VPC_1 and VPC_2 to enable seamless communication while ensuring isolation and data protection.
2.	Enable Subnet Accessibility: Ensure all subnets in VPC_2 are fully accessible from VPC_1, facilitating efficient inter-VPC communication.
3.	Maintain isolation and security: Ensure that VPC_1 and VPC_2 remain logically and physically isolated, minimizing the risk of security breaches.

### Optimization strategies:
*	Optimize Network Configuration: Simplify network architecture by leveraging VPC peering.
*	Minimize Costs: Implement an efficient setup that minimizes data transfer costs and avoids unnecessary resource usage.

### Core Components:
1.	Amazon Virtual Private Cloud (VPC): The foundational networking component that isolates resources within VPC_1 and VPC_2, each with its own CIDR block.
2.	VPC Peering Connection: A secure and scalable link established between VPC_1 and VPC_2 to enable inter-VPC communication.
3.	Route Tables: Updated to route traffic between VPC_1 and VPC_2 through the VPC peering connection, ensuring seamless connectivity.
4.	Security Groups: Configured to allow specific inbound and outbound traffic between resources in the two VPCs, maintaining fine-grained access control.
5.	EC2 Instances: Used to validate and test the VPC peering connection by simulating data exchange between VPC_1 and VPC_2.

## Step-by-Step Guide to Launch EC2 Instance Using CloudFormation
________________________________________
### Step 1: Log in to AWS Management Console
1.	Open a web browser and go to the AWS Management Console.
2.	Log in to your AWS account using your credentials.
 ![image](https://github.com/user-attachments/assets/8c97bb8c-460c-4f73-94e2-1f89eb8782fb)

### Step 2: Creating VPC:
1.	Open VPC service from services menu
 ![image](https://github.com/user-attachments/assets/3fa71a10-0335-435f-8c9c-cbd621447f06)


2.	Click on Create VPC.
3.	Select VPC only and provide a name (ex: vpc_1)
4.	Define the CIDR range for VPC (e.g., "12.0.0.0/16").
 ![image](https://github.com/user-attachments/assets/fd8e46af-d500-49b3-bd1d-12df01ea5b5e)

5.	Click on Create VPC.
 ![image](https://github.com/user-attachments/assets/d0a4ea2d-94c4-4520-ba03-a8669f6da005)

6.	Now Repeat the same steps for creating second VPC (ex: vpc_2) with a different CIDR range for not to overlap as overlapping ranges can cause routing issues.
 ![image](https://github.com/user-attachments/assets/1ade292e-2557-4800-9935-89042b235a62)
![image](https://github.com/user-attachments/assets/1f9bcf86-6bd1-45c7-a256-aad13178348b)

 
________________________________________







### Step 3: Creating Route tables:
1.	Navigate to Route tables on left section of VPC.
 ![image](https://github.com/user-attachments/assets/76536c06-1708-4ca1-bddf-abaeecbfa609)

2.	Name the route table (ex: rt_vpc_1).
3.	Select the first created VPC i.e., vpc_1.
 ![image](https://github.com/user-attachments/assets/23752047-645c-4724-a33c-b31782c50a2d)

4.	Click on Create route table.
 ![image](https://github.com/user-attachments/assets/4ec11377-595d-4bd8-901a-da9f03f8ba26)

5.	Now repeat the same steps for creating second route table for second vpc and name it (ex: vpc_2) and attach it to second created vpc i.e., vpc_2.
 
  ![image](https://github.com/user-attachments/assets/986365e5-0431-4daf-a1a0-317ce54f6c68)
  ![image](https://github.com/user-attachments/assets/c204281c-35ed-4216-9559-3a6d2a543b86)

 
________________________________________
### Step 4: Creating Subnets:
1.	Navigate to Subnets on left section of VPC.
 ![image](https://github.com/user-attachments/assets/f6883f36-6c6d-4cf1-a552-32673fc93c37)

2.	Click on Create Subnets.
3.	Select firstly created VPC i.e., vpc_1.
 ![image](https://github.com/user-attachments/assets/1adc1197-96e8-4161-90ac-d83dab48047e)

4.	Configure the subnet settings such as provide a subnet name (for ex: subnet_vpc_1_1a) and select the availability zone and provide CIDR block.

 ![image](https://github.com/user-attachments/assets/8daff111-bb16-462c-83c3-54db7e5b8371)

5.	Click on Create Subnet.
 ![image](https://github.com/user-attachments/assets/400806ad-9b05-4cdb-bf6c-3f5922a54b82)

6.	Now repeat the same steps for creating second subnet for second vpc and configure the subnet details such as name, availability zone and CIDR block.

![image](https://github.com/user-attachments/assets/ebb0eff8-ff72-4368-bb9c-e90b2660bd94)
![image](https://github.com/user-attachments/assets/30621d42-6d1f-4b0f-85fa-7903daf1b849)
![image](https://github.com/user-attachments/assets/c45958d2-5f3b-4740-841d-499cca791f48)

 
 
________________________________________
### Step 5: Setting Up Route Table:
1.	Navigate to route table of first vpc i.e., rt_vpc_1.
 ![image](https://github.com/user-attachments/assets/60ea12c2-2b76-4686-a11c-37b2e3c9425c)

2.	Go to subnet association section and click on Edit subnet associations.
3.	Select the first subnet i.e., subnet_vpc_1_1a. 
 ![image](https://github.com/user-attachments/assets/9146803e-7596-46bd-8d8e-1ef22988eea6)

4.	Click on Save associations.
 ![image](https://github.com/user-attachments/assets/5320020e-9906-4ae1-9f36-2e04a378fa15)

5.	Now repeat the same steps for second route table to associate the respected subnet i.e., subnet_vpc_2_1a.
![image](https://github.com/user-attachments/assets/054a3709-c6c6-418c-84db-2a7f92674784)
![image](https://github.com/user-attachments/assets/422f9b38-b251-4f7a-8fa4-0dcf31303a5c)
 
 
________________________________________
### Step 6: Configuring Internet Gateway:
1.	Navigate to Internet Gateway on left section of VPC.
 ![image](https://github.com/user-attachments/assets/4d36d13e-6e7b-4a4e-a9ad-d57cfa54cd0f)

2.	Click on Create Internet gateway.
3.	Provide a name tag (ex: igw_vpc_1) for attaching this internet gateway to first vpc. 
 ![image](https://github.com/user-attachments/assets/64191288-54b4-4215-8c26-378eee74019c)

4.	Click on Create Internet gateway.
 ![image](https://github.com/user-attachments/assets/c74df4d2-3005-4be5-8805-2a168e22ed5b)

5.	Click on Attach to a VPC.
6.	Select the first vpc i.e., vpc_1.
 ![image](https://github.com/user-attachments/assets/69ddddb8-9b83-4e06-b3b7-a50df3a1d8d9)

7.	Now repeat the same steps for creating internet gateway for second vpc by naming it (ex: igw_vpc_2) and attach it to second vpc i.e., vpc_2.
 
![image](https://github.com/user-attachments/assets/4350bbd3-7b80-44d8-b9a5-868656b92870)
![image](https://github.com/user-attachments/assets/3ab24048-d9f3-4d2a-9baf-5b65798f2c90)

 
________________________________________







### Step 7: Configuring Rote tables:
1.	Navigate to first route table i.e., rt_vpc_1 and click on edit routes.
 ![image](https://github.com/user-attachments/assets/c45d852b-6ae3-458f-9ec0-d0343ba3cf82)

2.	To allow subnet to access the internet, add a new route to the subnet route table with the following settings:
Destination: 0.0.0.0/0
Target: The internet gateway that you just created (I.e., igw_vpc_1)
 ![image](https://github.com/user-attachments/assets/0e81662f-6ed6-478d-a796-29bb72201987)

3.	Click on Save changes.
4.	Repeat the same steps for configuring the route table of second vpc and select the second internet gateway (i.e., igw_vpc_2).
 ![image](https://github.com/user-attachments/assets/383f3bf7-2405-4a28-a800-e1230f357a7e)

________________________________________
### Step 8: Creating EC2 instances:
1.	Open EC2 service from services menu.
 ![image](https://github.com/user-attachments/assets/3b1eb652-29ab-4b32-a610-9b447e7ad13d)

2.	Click on Launch Instance.
3.	Provide a name (for ex: vpc_1_ec2_instance).
4.	Select and AMI from Quick start section (for ex: Ubuntu).
 ![image](https://github.com/user-attachments/assets/7d966050-7cf1-493e-9032-d0a62a74893e)

5.	Create a key pair for secure login and name it (for ex: vpc_1_ec2_key).
 ![image](https://github.com/user-attachments/assets/2d6142a2-3cf4-43b1-800a-494d70ec9b5d)

6.	Configure network settings by selecting the first created vpc i.e., vpc_1.
7.	Select the subnet i.e., subnet_vpc_1_1a.
8.	Enable the Auto-assign public IP.
 ![image](https://github.com/user-attachments/assets/d4c7dca1-fd8d-4818-88bb-5084afc2ad76)

9.	Add an Inbound security group rule for HTTP, anywhere.
 ![image](https://github.com/user-attachments/assets/21b7b6b7-42a6-4153-a51c-2e72f44e05e3)

10.	Go to advanced settings section and provide the user data for installing Apache on EC2 instance.
 ![image](https://github.com/user-attachments/assets/4f4e16e3-2f2f-45d9-95de-500618ab309c)

11.	Click on Launch Instance.
 ![image](https://github.com/user-attachments/assets/98cdc9ac-1a0d-4414-8ca6-394ad7810aed)

12.	Now repeat the same steps for creating a second EC2 instance named vpc_2_ec2_instance and select the respective second vpc(i.e., vpc_2) and second subnet (i.e., subnet_vpc_2_1a).
 ![image](https://github.com/user-attachments/assets/e840a9c3-0166-4bf8-a449-51b851ea6be9)

________________________________________
### Step 9: Creating Peering Connection:
1.	Navigate to VPC service and select Peering connections from left section.
 ![image](https://github.com/user-attachments/assets/35b7fb75-0b77-4c41-9318-5562bba831a5)

2.	Click on Create peering connection.
3.	Provide a name (for ex: peering-connection-between-vpc1-and-vpc2).
4.	Select a vpc requester (i.e., vpc_1)
 ![image](https://github.com/user-attachments/assets/50212423-703b-4e6a-b20a-b5caab33d110)

5.	Select an accepter vpc (i.e., vpc_2).
 ![image](https://github.com/user-attachments/assets/d0612d48-bbd9-42bc-bbb7-eb131724cf82)

6.	Click on create peering connection.
 ![image](https://github.com/user-attachments/assets/ea20265f-5f0b-456b-822f-7ba26752c7dc)

7.	Select Actions and accept the request.
 
   ![image](https://github.com/user-attachments/assets/2a5cb1d9-dfd7-4596-bd1b-ef1e4f83810f)

8.	Click on Modify my route tables now.
 ![image](https://github.com/user-attachments/assets/e53b4d07-4c31-4c77-8aac-afd5e476dc1c)

9.	Go to route table of first vpc (i.e., rt_vpc_1) and click on Edit routes.
10.	Add IP of vpc_2 and the target as "VPC Peering".
 ![image](https://github.com/user-attachments/assets/b782d46a-d4db-4d4a-b5e4-82daac4e9b98)

11.	Repeat the same for second route table (rt_vpc_2) and add IP of vpc_1.
 ![image](https://github.com/user-attachments/assets/8a88edcd-aeed-40e8-9113-dc12c3f9c18f)

________________________________________
### Step 10: Connecting to EC2 instance:
1.	Navigate to EC2 instance.
 ![image](https://github.com/user-attachments/assets/98cbaea9-9040-479c-8e22-34885b98a671)

2.	Select vpc_1_ec2_instance and click on connect.
 ![image](https://github.com/user-attachments/assets/4856bad4-832e-4fc2-88db-bfc7d4dd97ea)

3.	Copy the SSH command and Open SSH and run the command and type yes.
 ![image](https://github.com/user-attachments/assets/9ac53dfd-2f5c-48e1-bcf7-222af1a64615)

4.	Now curl the second from this first instance by running the curl command followed by IP of second instance.
 ![image](https://github.com/user-attachments/assets/de29e32c-8ef4-4964-9113-92b598ee5e35)

5.	Repeat the same steps by connecting to vpc_2_ec2_instance and curl the first instance with the respective IP.
 ![image](https://github.com/user-attachments/assets/d9b1d117-1055-403a-956d-f53eaf4c300f)
![image](https://github.com/user-attachments/assets/9b453473-a535-4636-bb43-1ea2800dd9af)

 
By following the mentioned steps, we can create a peering connection between two VPCs.

________________________________________

### Best Practices Implemented:
1.	Non-overlapping CIDR Blocks: Ensured that the CIDR blocks of VPC_1 and VPC_2 do not overlap to prevent routing conflicts and connectivity issues.
2.	Selective Route Table Updates: Updated only the necessary route tables to minimize impact on unrelated subnets and maintain efficient routing.
3.	Security Group Rules: Implemented strict security group rules to control traffic flow between the VPCs, allowing only necessary communication.
4.	Cost Optimization: Evaluated and minimized data transfer costs by directly connecting the VPCs through peering instead of using NAT gateways or VPNs.

### Benefits:
* Enhanced Connectivity: Enabled seamless and direct communication between resources in VPC_1 and VPC_2, eliminating the need for additional intermediaries like VPNs or Transit Gateways.
* Improved Performance: Optimized data transfer with low-latency routing, ensuring efficient operations across the connected VPCs.
* Scalability: Established a scalable network configuration, allowing for the addition of more resources or subnets in the future without connectivity issues.
* Cost Efficiency: Reduced infrastructure costs by avoiding the need for complex networking setups like Transit Gateways, while ensuring efficient use of AWS resources.

### Conclusion
This project successfully implemented a secure and efficient VPC peering connection between VPC_1 and VPC_2, enabling seamless communication between all subnets in VPC_2 from VPC_1. This solution ensures a robust network configuration that adheres to AWS best practices for security, scalability, and cost efficiency. The successful implementation of this solution will enable the organization to leverage the full potential of AWS's cloud services and drive further innovation and growth.
