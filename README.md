# AWS_Developer_Certification


# IAM: 
1) Controls who can access your AWS environments.
2) Controls what they can do 
3) Global


Benifits of using IAM
1) Shared across your AWS account
2) Central control of your account
3) Granular API level permissions
4) Identity federation
5) Temporary credentials to users/application

# Virtual private cloud

Virtual network that closely resembeles a traditional private data center, with the benifits of using the AWS scalable infrastucture
Logically isolated from the other virtual networks in the cloud.
Launch AWS resources within your VPC.

You have number of options for connecting into VPC.

1) Hybrid cloud approach - Create a VPN connection between on premise datacenter and your VPC to extend your network. You have complete control over your virtual networking environment. Like the selecting of the IP address ranges, creation of the SUBNETS, configuration of the route tables and the network gateways 
2) A Single VPC exists within a region, across multiple availability zones. 
    1 VPC -> 1 Region -> Multiple AZ's 
    VPC are not cross-region. 
    Indivoidual regions should have their own VPC's, if you want to deploy a multi region application.
    VPC -> Region is one-to-one
    VPC -> Availability zone is one-to-many
3) VPC is free to use, but you gotta pay for the resources within the VPC. Resources include, VPN connection-hours & NAT gateways.

Advantages of VPC: 
Provides advanceced security features. Ex: Security groups, NACL to enable inbound and outbound filtering at the instance level and the subnet level.

Sample Use cases: 
a) Hosting simple public websites.
You certainly don't want the DB to be public, so place your DB instance in the private subnet within the VPC. Then your DB will be only accessed by the server running your website. 
b) Hosting multi-tier apps
Ex: In banking domain, A Mainframe application deals with the core processing while the other application are sitting in the cloud will make calls to the mainframe application. Like to get balance, history of user debit. 
VPC is responsible to route these calls in between these applications. 
c) Hosting scalable web application in the cloud, serverless applications. 
d) Diaster Recovery


Specify a range ipv4 addresses for the VPC in the form of a classless inter domain routing (CIDR) block.
Ex: 10.0.0.0/16

AWS recommend you to specify a CIDR block from the private IPV4 ranges:
```
a) 10.0.0.0. - 10.255.255.255 (10/8 Prefix)
b) 172.16.0.0. - 172.31.255.255 (172.16/12 Prefix)
c) 192.168.0.0 - 192.168.255.255 (192.168/16 Prefix)
```

1 VPC --> 1 CIDR block one-to-one mapping. 

Allowed block size is between a /16 netmast and /28 net mask.
16 to 65,536 IP addresses

# TODO: Yet to read about IPv6 & CIDR association.

# Subnet

A subet is a range of IP addresses in your PC
Public subnet -> for the resources that must be connected to the internet. Ex: Webserver
Private subnet -> for the resources that should not be connected to the internet. Ex: A Database. 
A subnet must reside entirely within one availability zone. SUBNET -> Availability zone, ONE-TO-ONE relation ship.
A subnet cannot span across multiple AZ's
By default, 
  1) all subnets within a VPC can route traffic to one another 
  2) The first 4 IP addresses and the last IP addresses in each subnet CIDR block are not allowed to be used. They are resrved for AWS        infrastructure.
  3) They represent: Network address, VPC router addresses, DNS server address, address for future use, last address -> network broadcast address. If you want to broadcast something to all the nodes or all the devices with in the subnet, you can go with the network broadcast address. 

A subnet must be associated with a route table, which specifies the allowed routes for outbound traffic leaving the subnet. 
Newly created subnets are automatically associcated with the main route table for the VPC. However if you want to create a public & a private segregation between our subnets we need to create custom route tables. 

# Internet gateway.

Horizontally scaled, redundant and highly availble VPC component that allows communication between the instancres in your VPC & the internet. 
Public Subnet -> Subnet's traffic is routed to an IGW. -> This is the default behavior. Default VPC & Default IGW. /16 IPV4 CIDR Block
Private Subnet -> Subnet's traffic is not routed to an IGW.

Max 1 IGW for a VPC.

NACL: Acts as a firewall at the subnode level. It controls both inbound & outbound traffic at the subnet level.
Security Groups: Acts as a firewall at the Amazon EC2 instances, controlling both inbound & outbound traffic at the instance level.

Default VPC:
1 IGW is connected to your VPC.
All subnets are public and are associated with the main route table and sends the internet traffic to the IGW.
Instances launched into the default subset receive both a public IPV4 address and a private IPV4 address.
Instances in a default subnet also receive both publie and private DNS hostnames

# NACL - Network access control list



# Fully managed SQL Databases - RDS

RDS - Relational database service. 
RDS uses EBS volues for database and log storage. 

# Route 53 & DNS


