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






