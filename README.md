# **Project: Dynamic Scaling in AWS Auto Scaling.**

## _Project Goals:_

1. Understand the given Architecture Diagram
2. Create the infrastructure
3. Ensure your infrastructure is splitted across multiple zone in a silgle region
4. Deploy a simple Node.js application to the infrastructure
5. Load test the application
6. Ensure the Auto-scaling group increase the instance when the CPU usage rises to 80%
7. Ensure the Auto-scaling group increase the instance when the Memory usage rises to 80%
8. Ensure the Auto-scaling group scales down when the load decreases
9. Ensure you DELETE all you resources after you are done.

# **Architecture Diagram**

![Architecture Diagram](images/diagram.JPG)

# _Step-by-Step Implementation:_

## Step 1: Understand the Architecture Diagram

### _The architecture should include:_

- An Application Load Balancer (ALB) to distribute traffic.
- Auto Scaling Groups (ASGs) to manage EC2 instances.
- EC2 instances running the Node.js application.
- CloudWatch for monitoring CPU and memory usage.
- Multiple Availability Zones (AZs) for high availability.

## Step 2:Create the Infrastructure

### 2.1 Set Up the VPC and Subnets

- Create a VPC and multiple subnets in different availability zones within the same region.
  ![VPC](images/createvpc.JPG)
- Create an Internet Gateway, Attach it to your VPC.
  ![Gateway](images/createattagtw.JPG)
- Create Route Tables and associate it with the public subnets.
  ![Create Routetable](images/route2.JPG)
  ![attached routetable](images/route1.JPG)
- Add a route to the internet gateway.
  ![attached gateway](images/attgtw.JPG)

### 2.2 Create Security Groups

- Create a security group to allow HTTP (port 80) and SSH (port 22) access.
  ![Securitygroup](images/attachldb.JPG)
- Create a Security Group for EC2 Instances,allow inbound traffic from the load balancer security group, allow outbound traffic to the internet.
  ![Add rule first EC2](images/addEC21.JPG)
  ![Add rule 2](images/addEC22.JPG)

### 2.3 Set Up the ALB

Create an Application Load Balancer.

1. Create a Load Balancer:

- Go to the EC2 Dashboard and select "Load Balancers".
- Click on "Create Load Balancer" and choose "Application Load Balancer".
- Configure the load balancer, select the VPC, and the public subnets.

2. Configure Listeners and Target Groups:

- Create a target group for your EC2 instances.
- Register your EC2 instances with the target group.

### 2.4 Launch EC2 Instances

Create a launch template for your EC2 instances.'launch-template-data.json' should include the AMI ID, instance type, key name, security groups, and user data to install Node.js and your application.

### 2.5 Create an Auto Scaling Group

Create an Auto Scaling Group that uses your launch template and spans multiple subnets.

## Step 3: Deploy the Node.js Application

Deploy your Node.js application to the EC2 instances. Use the user data section in the launch template to automate the deployment.

## Step 4: Configure Database Connectivity

Set up a secure connection between AWS and the on-premises database using AWS Direct Connect or a VPN. Update the application configuration to connect to the on-premises MySQL database using its private IP address.

## Step 5: Implement Security Best Practices

Encrypt data in transit using SSL/TLS for communication between the application and the database.

Set up IAM roles to manage permissions and access controls for AWS resources.

## Step 6: Monitoring and Logging

Set up CloudWatch to monitor application performance and resource utilization. Enable CloudTrail for logging and auditing AWS API calls.

## Step 7: Load Testing

Use a tool like Apache JMeter or Artillery to simulate load and test the application.

## Step 8: Scale Up and Scale Down

Ensure the Auto Scaling Group scales up when CPU usage rises to 80%.Ensure the Auto Scaling Group scales down when the load decreases.

## Step 9: Clean Up

Delete all resources to avoid unnecessary costs.
