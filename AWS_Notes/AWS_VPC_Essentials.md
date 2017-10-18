 AWS Definition: “Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the Amazon Web Services (AWS) cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets and configuration of route tables and network gateways.”

Note: When you create an AWS account, a “default” VPC is created for you, including the standard components that are needed to make it functional.
1) Internet Gateway (IGW)
2) A route table (with predefined routes to the default subnets)
3) A Network Access Control List (with predefined rules for access)
4) Subnets to provision AWS resources in (such as EC2)


Internet Gateways (IGW)

AWS Definition: “An Internet gateway is a horizontally scaled, redundant and highly available VPC component that allows communication between instances in your VPC and the Internet. It therefore imposes no availability risks or bandwidth constraints on your network traffic.”

IGW rules you need to know:
1) Only 1 IGW can be attached to a VPC at a time.
2) An IGW cannot be detached from a VPC while there are active AWS resources in the VPC (such as an EC2 instance or RDS Database)

Route Tables (RTs)

AWS Definition: “A route table contains a set of rules - called routes - that are used to determine where network traffic is directed.”

 Route table rules you need to know:
1) Unlike an IGW, you can have multiple “active” route tables in a VPC
2) You cannot delete a route table if it has “dependencies” (associated subnets)

Network Access Control List (NACLs)

AWS Definition: “A network access control list (NACL) is an optional layer of security for your VPC that acts as a firewall for controller traffic in and out of one or more subnets.”

nbound & Outbound Rules:
(1) Rules are evaluated based on “Rule #” from lowest to highest.
(2) The first rule evaluated that applies to the traffic gets immediately applied and executed.

(3) For the “default” NACL, ALL Traffic is allowed (both inbound/outbound).
(4) “New” NACL: When you create a new NACL, ALL Traffic is DENIED by default.

Note: Inbound SSH traffic will always be on port 22. However, outbound SSH traffic can use “ephemeral” ports - which include TCP ports 1024-65535. To prevent connectivity issues with EC2 instances, allow all ports ranges on NACL outbound rules.

(5) A subnet can only be associated with ONE NACL at a time.
(6) A NACL allows or denies traffic from entering a subnet. Once inside the subnet, other AWS resources (i.e. EC2 instances) may have an additional layer of security (security groups.)

Subnets

AWS Definition: “When you create a VPC, it spans all of the Availability Zones in the region. After creating a VPC, you can add one or more subnets in each Availability Zone. Each subnet must reside entirely within one Availability Zone and cannot span zones.”

(1) Subnets MUST be associated with a route table.
(2) A PUBLIC subnet HAS a route to the Internet.
(3) A PRIVATE subnet does NOT have a route to the internet.
(4) A subnet is located in ONE specific Availability Zone.

Availability Zones (VPC Specific)

AWS Definition:
“When you create a VPC, it spans all of the Availability Zones in the region. After creating a VPC, you can add one or more subnets in each Availability Zone. Each subnet must reside entirely within one Availability Zone and cannot span zones.”

Availability Zones are distinct locations that are engineered to be isolated from failures in other Availability Zones. By launching instances in separate Availability Zones, you can protect your applications from the failure of a single location.

High Availability: Creating your architecture in such a way that your “system” is always available (or has the least amount of downtime possible).

Fault Tolerant: The ability of your “system” to withstand failures in one (or more) of its components and still remain available.

 Q: What is the proper structure of AWS Global Infrastructure?
A: Regions -> Availability Zones -> Data Centers -> AWS Services

T: A VPC is your private, logically isolated section of AWS.

T: Route Tables are what direct the flow of traffic between resources within a VPC.

Q: Availability Zones allow for this type of cloud architecture?
A: Highly available and fault tolerant architecture.

T: An Internet Gateway MUST be attached to a VPC for AWS resources, such as an EC2 instance, to have access to the Internet.

Q: What is the security layer that allows/denies data from entering or exiting a subnet?
A: Network Access Control List (NACL)

Q: VPC is an abbreviation for:
A: Virtual Private Cloud

 VPC Essentials

CDN = Content Delivery Network

VPC Network Routing Basics

A PUBLIC subnet HAS a route to the Internet (it is associated with a route table that has an IGW attached)
A PRIVATE subnet does NOT have a route to the Internet (it is associated with a route table that does NOT have an IGW attached)

VPC Security Basics

NACLs: Best practice to increment numbers by 10, so if you have to place a rule in a certain order, it does not create an issue.

Security groups: Are security for the instance level. They support only ‘allow’ rules. Best practice is to allow ONLY traffic that is required.

VPC Basics Quiz

T: For a subnet to be considered public, it must have a route to the Internet. Having a route to the Internet means that it must be associated with a route table that points to the IGW.

Q: You have been tasked with auditing the security of your VPC. As part of this process, you need to start by analysing what traffic is allowed to and from various EC2 instances. What two parts of the VPC do you need to check to accomplish this task?
A: Security Groups and NACLs
E: Security Groups and NACLs are the two parts of the VPC Security Layers. Security Groups are a firewall on the instance level, and NACLs are a firewall on the subnet level.

Q: What best describes how NACLs rules work?
A: Rules are evaluated by rule number, from lowest to highest, and executed immediately when a matching allow/deny rule is found.

T: A VPC can only have one IGW attached at a time.

Q: If data is travelling from a customer, over the open Internet, to a web site you are hosting on an EC2 instance in an AWS VPC, what is the order of components that data will travel through?
A: IGW -> Route Table -> NACL -> Subnet -> Security Group -> EC2 Instance

Q: You work for a financial institution that is preparing to (possibly) migrate their on-premise infrastructure to AWS. As part of this process, you have been tasked with preparing the cloud strategy that will be presented to your CTO. As part of this presentation, you need to highlight several of the top benefits of using an AWS VPC. Which of the following benefits do you highlight in this section of the presentation?
A: The ability to have both public and private subnets
A: The ability to extend your on-premise network to the cloud via VPN
A: The ability to provide a DNS server for your VPC

Q: Your company’s management team has been considering moving their on-premise network to AWS. You have been called into a meeting to brief the management team on some specifics of AWS. One of the first questions you are asked is what exactly a VPC is. How should you respond?
A: An AWS VPC closely resembles a traditional on-premise network, with the added benefit of AWS infrastructure.

T: NACLs are stateless, and security groups are stateful.
E: NACLs are stateless, which means that return request traffic must have an allow rule set up for that return traffic to enter or leave the subnet. Security groups are stateful, which means that return request traffic does not need an allow rule set up for that return traffic to enter or leave the security group.

Q: You are the lead Solutions Architect for a healthcare company and are managing an application running on multiple EC2 instances. Those EC2 instances must have the ability to access other AWS resources. What is the best way to manage this access?
A: Use an IAM role to manage temporary credentials for applications that run on an EC2 instance. The role will supply temporary permissions that applications can use when they make calls to other AWS resources.

T: All subnets, regardless of being public or private, can communicate with each other inside of a VPC.
E: Since each route table has a local target with the destination of the VPCs CIDR block range, all subnets within a VPC can communicate with each other.

T: In the default VPC, all subnets have a route to the Internet.









