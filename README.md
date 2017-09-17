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
1. 1 IGW is connected to your VPC.
1. All subnets are public and are associated with the main route table and sends the internet traffic to the IGW.
1. Instances launched into the default subset receive both a public IPV4 address and a private IPV4 address.
1. Instances in a default subnet also receive both publie and private DNS hostnames

## EC-2

##### EC-2 Tagging
Tag as much as possible, tags as used to patrol the costs and to see where your costs are coming from. 
Once you are able to login, make userself a SUPER USER by issuing the following command. **sudo su**

##### Create new EC-2 instance and host a simple HTML page.
Once you create the EC2 instance, you will be using the **public ip-address** to SSH to the machine. 
In windows:
Putty: ec2-user@public-ip-address
In Mac:
**ec2-user@public-ip-address -i XXXX.pem** file
add the PPK key in the AUTH section. 
and you will be able to login to that machine. 

Once you login, create a web-page **index.html** and start the webserver using the following command.
**service httpd start**
Following command is to make the APACHE started once the instance is started. 
**chkconfig httpd on**
Use the public DNS to see the webpage.


##### Reserved EC-2 instance
Reserved instances can be created using AWS. It's like you are setting your own server for your self.

##### Storage encyrption with-in EC-2 instance
When creating EC2 instances, you have an option for selecting **STORAGE**. 
You cannot encyrpt root/default storage, 
You can envrypt the other storage types.

Exam-TIPS:


# NACL - Network access control list


# Fully managed SQL Databases - RDS

RDS - Relational database service. 
RDS uses EBS volues for database and log storage. 

# Route 53 & DNS

# Security Group
When creating the security groups, there are three options in the **Sources** section.
1. Custom
1. Anywhere
1. My IP - You can actually restrict **SSH** down to your own individual IP address. IP/32

![Scurity-groups](https://i2.wp.com/venkatad.files.wordpress.com/2017/08/security-group-ip-address.jpg?ssl=1&w=450)


Create a Key-pair
Public key - is a pad lock
Private key - is the key that unlocks that pad lock. 
You can use public key on multiple EC2 instances. You are putting a pad lock on all your virtual machines in the cloud. And with the PRIVATE key you can unlock those pad lock. 

**Exam-tip**: 
1. Any change in the security group or in the rules that are associated with the security group are applied immediately. 
1. Security groups are **stateful** -> once you add the inbound rules the outbound rules are added automatically. Everything you allow in will go out automatically.
1. We cannot deny the traffic, deny the IP addess with the security group. You can do it with the NACL.
1. You can associate multiple security groups to one EC2 Instances.


**Stateful** -> Outbound rules are added automatically with the inbound rules. Ex: Security Groups
**Stateless** -> Outbound rules are not automatically added with the inbound rules, You need to manually add them. Ex: NACL

# Upgrading the EBS volume types
Now we will work on creating the new volumes and attaching to the EC2 instances. 

Create a snapshot. 
Volumne types used 
1. Standara -> Magnetic.
1. gp2 -> General purpose 
1. io1 -> Provisional 

```
[root@ip-XXXXX /]# lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk
└─xvda1 202:1    0   8G  0 part /
**xvdf**    202:80   0   8G  0 disk
[root@ip-XXXXX /]# file -s /dev/xvdf
**/dev/xvdf: Linux rev 1.0 ext4 filesystem data, UUID=0dd53590-f55f-45c4-8c81-74ef1fa5cead (extents) (large files) (huge files)**
[root@ip-XXXXX /]#
```

# AMI Amazon
We can see these are snapshots of virtual machines that you can provision and boot up.
There are two kinds of virtualization 
    1. HVM - hardware virtual machine
    1. PV - paravirtual




The below command will mount to the /efs location. If we need to mount to another location change it to the desired location.
```
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 fs-6fea8726.efs.us-east-1.amazonaws.com:/ efs
```


# SQS -> Decouple your infrastructure. 
SQS, is what they are looking for.

Exam-Tips:
1. SQS Delivery: SQS messages can be delivered multiple times in any order. 
###### You might get a question when you want to process or prioritize the messages in the queue. If you want to process a set of messages faster than the other, you need to create two queues. Queue-A which will get higher priority by replication and queue-b will get lower priority. 
1. Default visibility time out is 30 seconds. Maximum time out is 12 hours.

###  SQS vs SNS is popular exam topic.

## CLI Commands - for the developer exam.


aws configure

Describe the instances that you provisioned.

describe-instances
describe-images

start-instance
run-instances

If you want to start a new instance. 
**aws ec2 run-instances --image-id ami-XXXXX --count 1 --instance-type t2.micro --key-name KEYNAME --security-group-ids sg-XXXXX --subnet-id subnet-XXXXX**

**aws ec2 terminate-instances --instance-ids i-XXXXXXXXXXXXX**


**Exam Topic 
SNS data format is : JSON
Subscription will be cancelled with in 3 days.
**



