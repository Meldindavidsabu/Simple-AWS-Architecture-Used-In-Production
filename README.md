# A Simple AWS Architecture Used In Production
A simple AWS Architecture which is deployed in two availability zones and is consisting of  VPCs, subnets, security groups, auto Scaling, Load Balancers, NAT gateways and a bastion host.

**Introduction: Crafting Resilient AWS Architecture**

In the realm of Amazon Web Services (AWS), building a robust and dynamic architecture is an art that combines various components into a symphony of reliability, security, and scalability. This project embraces the canvas of the cloud, seamlessly weaving together an ensemble of components to create an architecture that stands strong in the face of challenges.

At its core, this revolves around the concept of a Virtual Private Cloud (VPC) - a virtual network environment where the entire ecosystem unfolds. This VPC encompasses multiple Availability Zones (AZs), distinct geographic regions housing AWS resources. Each AZ is a fortress of computational resources, ensuring that the infrastructure remains resilient even in the presence of failures.

Within this VPC, we venture into the realms of subnets - segmented areas within the AZs. These subnets, both public and private, form the foundation upon which the architecture is built. Public subnets, poised at the edge, engage directly with the internet, hosting components like Load Balancers that distribute incoming traffic across internal resources.

Security stands as a sentinel in this landscape. Security Groups, like ethereal guardians, define access to resources. They regulate the flow of traffic, enabling safe and secure communication between various components. Whether it's the bastion host, a gateway to secure communication, or the EC2 instances, their interactions are carefully governed by these security groups.

Speaking of EC2 instances, their creation and management are elevated through Auto Scaling. This mechanism dynamically adjusts the number of instances in response to changing demands, ensuring that the architecture scales gracefully, never faltering under the weight of traffic surges.

Amidst these interwoven threads, the project introduces NAT Gateways, acting as bridges to the external world, while Route Tables navigate the traffic, routing it to the right destinations. Each component, meticulously placed, adds depth to the architecture's design.

In this orchestration of technology, the project's objective is clear: to forge an environment that embodies resiliency, security, and scalability. Through Availability Zones, VPCs, subnets, security groups, Auto Scaling, Load Balancers, NAT gateways, and more, this AWS architecture emerges as a harmonious composition, ready to weather challenges and inspire confidence.

**Step 1: Create a VPC with "VPC and More" Wizard**
1. Log in to the AWS Management Console.
2. Navigate to the VPC dashboard.
3. Click "Launch VPC Wizard" and select "VPC with Public and Private Subnets."
4. Choose the desired configuration, including the number of AZs and subnets in each.
5. Configure IPv4 and optionally IPv6 CIDR blocks.
6. Enable DNS hostnames and resolution for seamless communication.
7. Review the configuration and create the VPC.

**Step 2: Create Security Groups**
1. In the EC2 dashboard, access the "Security Groups" section.
2. Create a security group for your EC2 instances in the private subnet.
   - Name it as "PrivateInstanceSG."
   - Configure inbound rules for required ports (e.g., SSH, application-specific).
3. Create a security group for your load balancer in the public subnet.
   - Name it as "LoadBalancerSG."
   - Set inbound rules for HTTP (port 80) and HTTPS (port 443).

**Step 3: Create Auto Scaling Templates**
1. In the EC2 dashboard, navigate to "Auto Scaling Groups."
2. Create an Auto Scaling launch template for EC2 instances.
3. Configure instance settings, such as AMI, instance type, key pair, and IAM role.
4. Associate the "PrivateInstanceSG" security group.
5. Specify user data scripts, if needed, for instance initialization.

**Step 4: Set Up Auto Scaling Groups**
1. Create an Auto Scaling Group for instances in private subnets.
2. Select the launch template created earlier.
3. Configure scaling policies based on metrics like CPU utilization.
4. Set desired, minimum, and maximum instance counts.
5. Associate the ASG with private subnets and the "PrivateInstanceSG" security group.

**Step 5: Create a Load Balancer**
1. In the EC2 dashboard, navigate to "Load Balancers."
2. Click "Create Load Balancer."
3. Choose "Application Load Balancer."
4. Configure listeners for HTTP (port 80) and HTTPS (port 443).
5. Select the public subnets created through the "VPC and More" wizard.
6. Set up health checks and define routing rules for target groups.

**Step 6: Set Up Bastion Host**
1. Launch an EC2 instance in a public subnet.
2. Assign the security group allowing SSH access (port 22) to the bastion host.
3. Use a key pair to securely access the bastion host.
4. This bastion host enables SSH tunneling for communication to private instances.

**Step 7: Configure Route Tables**
1. In the VPC dashboard, navigate to "Route Tables."
2. Create separate route tables for public and private subnets.
3. Associate the public route table with public subnets, with a default route via the Internet Gateway.
4. Associate the private route table with private subnets.

**Step 8: Configure Security Groups**
1. Modify security group rules to allow necessary traffic flows.
2. Allow inbound traffic for the load balancer security group (e.g., HTTP/HTTPS).
3. Configure security group rules for instances to communicate with each other.

By meticulously following these steps, your AWS project forms a comprehensive architecture. The "VPC and More" wizard takes care of NAT gateway creation, while Auto Scaling templates elevate the orchestration of EC2 instances. This alignment complements the holistic architecture enveloping Availability Zones, VPC configurations, security groups, Load Balancers, bastion hosts, route tables, and refined security rules.
