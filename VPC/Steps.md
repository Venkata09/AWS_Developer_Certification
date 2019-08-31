Amazon VPC lets you provision a logically isolated section of the Amazon Web Services (AWS) cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address ranges, creation of subnets, and configuration of route tables and network gateways.

Amazon VPC comprises a variety of objects that will be familiar to customers with existing networks:

    Subnet: A segment of a VPC’s IP address range where you can place groups of isolated resources.
    Internet Gateway: The Amazon VPC side of a connection to the public Internet.
    NAT Gateway: A highly available, managed Network Address Translation (NAT) service for your resources in a private subnet to access the Internet.

Let’s design our VPC diagram as follow:

![https://miro.medium.com/max/1720/1*CAoNZcAgIWryakepIAO8KA.jpeg]()


We have to decide the design for the VPC base on the requirement.Here we are going to create VPC with two private subnets and two public subnets as mentioned in the above diagram. Let’s do the implementation step by step.

Step 01 : Design the VPC architecture

Decide the IP range for the VPC before creating the VPC. Here we are using 10.1.0.0/24 as the CIDR block.This CIDR block assigns 256 IP address for the VPC. Hence we are using 4 subnets for the VPC we have to divide the 256 IP addresses among 4 subnets. I’ll explain how to calculate number of IP addresses for the VPC and divide them between subnets.

    CIDR block for the VPC -> 10.1.0.0/24

    Number of IP address -> 2^(32–24) -> 2⁸ -> 256

    Assuming equal number of IP addresses for the each subnet,

    Number of IP addresses for a subnet = 256/4 = 64

    Here is the IP address distribution for the above 4 subnets

    Public Subnet 1 -> 10.1.0.0/26 (IP range — 10.1.0.0–10.1.0.63)

    Public Subnet 2 -> 10.1.0.64/26 (IP range — 10.1.0.64–10.1.0.127)

    Private Subnet 1-> 10.1.0.128/26 (IP range — 10.1.0.128–10.1.0.191)

    Private Subnet 2 ->10.1.0.192/26 (IP range — 10.1.0.192–10.1.0.255)

We are going to implement VPC according to the above details

Step 02 : Log in to AWS management console

Log in to the AWS management console and go to the VPC under Services.

Step 03 : Create VPC

Go to “Your VPCs” in the side bar and Click on the “Create VPC “. This will pop up a window for the VPC creation. Add a name and CIDR block (10.1.0.0 /24 according to our example) for the VPC. Keep other fields with default values. Finally create the VPC.

Note : VPC belongs to only one region.



