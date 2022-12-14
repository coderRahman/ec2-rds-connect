# Create ec2 and rds instance and connect them

# Overview

The figure below shows what our final architecture will look like. We will create a VPC with 2 subnets in the us-east region. 1 public subnet in the us-east-1a availability zone and 1 private subnet in the us-east-1b availability zone. The VPC will have an Internet gateway attached,  the main route table will contain only a single local route that enables communication within the VPC. The public subnet will have a custom route table that includes the local route as well as a route directing all other traffic over the Internet gateway. A mysql RDS instance will be provisioned in the private subnet with an attached security group that only allows inbound traffic on port 3306 from the public subnet. An EC2 instance will be provisioned in the public subnet with an attached security group that only allows inbound SSH traffic from local IP and all outbound traffic. Finally, we will SSH into the EC2 instance, install the mysql client in public subnet instance and connet to mysql-instance using mysql command.

![My Image](images/main_pic.png)

#  Create a vpc 
## VPCs and subnets

A virtual private cloud (VPC) is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud. You can specify an IP address range for the VPC, add subnets, add gateways, and associate security groups.<br/>

A subnet is a range of IP addresses in your VPC. You launch AWS resources, such as Amazon EC2 instances, into your subnets. You can connect a subnet to the internet, other VPCs, and your own data centers, and route traffic to and from your subnets using route tables.

## Search vpc in aws search box, then navigate to vpc dashboard (To know about vpc search in google)

![My Image](images/vpc.png)

# Create internet gateway and attach to vpc

 Internet gateway allows communication between your VPC and the internet

![My Image](images/internet_gateway.png)

![My Image](images/attach_ig.png)

# Create a Custom Route Table

![My Image](images/custom_rt.png)

# Add route to route table for the internet gateway

![My Image](images/add_route.png)

# Create a public subnet in us-east-1a availibilty zone 
it will be used in ec2 instance

![My Image](images/public_subnet.png)


# Create a private subnet in us-east-1b availibilty zone
it will be used in rds instance

![My Image](images/private_subnet.png)

# Navigate to route table for the previously created public subnet. click custom route table and edit subnet association

![My Image](images/edit_subnet_1.png)
![My Image](images/edit_subnet_2.png)

# Create a security group for the EC2 instance to be provisioned in the public us-east-1a subnet.

Authorize inbound SSH traffic from your local IP address.

![My Image](images/ec2_sg.png)

# Create a security group for the mysql rds  instance to be provisioned in the private us-east-1b subnet.

Authorize inbound tcp traffic from the public subnet over port 3306.

![My Image](images/rds_sg.png)

# Launce a Ec2 instance

Edit network setting. <br/>
select previously created vpc and public subnet.<br/>
enable auto assign public ip<br/>
select previously created security group.<br/>

![My Image](images/ec2_1.png) <br/>

![My Image](images/ec2_2.png)


# Create database

select previously crreated vpc <br/>
public access -> no <br/>
choose existing security group and select mysql-rds-sg that created previously.<br/>

![My Image](images/mysql_1.png)

![My Image](images/mysql_2.png)

![My Image](images/mysql_3.png)

![My Image](images/mysql_4.png)

![My Image](images/mysql_5.png)

![My Image](images/mysql_6.png)

# Connect ec2 using ssh
 firstly change key file permission to 400
![My Image](images/connect_ssh.png)

# Install mysql-client in ec2
# Connect to mysql instance 

![My Image](images/connect_mysql.png)