## Virtual Private Cloud - VPC
1. creates a virtual network. It resembles a private datacenter or a private corporate network
1. If you delete default VPC, the only way you can get it back is by contacting AWS
1. default vpc is created upon instance creation. Now by default all ec2 is launched under a vpc.dfault vpc is connected to internet by default. It replaces ec2 classic functionality
1. Instances in VPC behave as if they were on the same private network
1. VPCs can be peered. Peering is in a star config, ie 1 central vpc
1. VPC peering can be done with vpc in the same region only
1. no additional charges for vpc, underlying services are charged as usual
1. size of vpc between /28 (14 Ip addresses) and /16
1. to change vpc size, you have to terminate and startover
1. amazon vpc does not support multicast and broadcast
1. you can assign multiple ip addresses
1. instances without Elastic IP address can access internet in two ways
1. via a NAT instance. they can use EIP of nat instance. Nat allows outbound connections, but does not allow internet to initiate connection to these machines
1. for vpc with hardware vpn, via virtual private gateway to existing data center
### Components of VPC
1. VPC
1. subnet
1. internet gateway
1. NAT instance: an ec2 instance that provides port address translation for non-eip instances to access internet via the gateway
1. hardware VPN
1. virtual private gateway : amazon side of a vpn connection
1. customer gateway : customer side of vpn connection
1. router to interconnect subnets and direct traffic between internet gateway , virtual private gateway, nat and subnets
### Benefits of VPC
1. Ability to launch instances into a subnet (range of ip)
1. Ability to define custom ip address ranges inside each subnet
1. Ability to configure route tables between subnets
1. ability to configure internet gateways and attach them to subnets
1. create layered network of resources
### VPC limits
1. 5 VPC per region, more on request
1. 5 internet gateways per account, equal to VPC limit
1. 5 virtual private gateways and 5 customer gateways
1. 1 internet gateway attached to a subnet at a time
1. 1 subnet can only be in 1 availability zone
1. 50 customer gateways per region
1. 50 VPN connections per region
1. 200 route tables per region
1. 200 subnets per amazon vpc
1. 5 elastic IP addresses
1. 100 security groups
1. 50 rules per security group
1. VPC via public subnet is accessible over internet. VPC via private subnet is not accessible over internet, atleast not without NAT (network address translation)

1. CIDR: Classless Inter Domain routing: specifies what your continuous IP address range is
1. You cannot create a VPC larger than /16
1. Tenancy: Default vs dedicated. Default is shared with others, dedicated means hardware is dediacated for you. the underlying hypervisor is dedicated in dedicated tenancy
1. if EC2 choose a dedicated vpc, automatically EC2 will be created as a dedicated. similar for any resouce which choosed a dedicated vpc
1. You can create subnets in different availability zones for highly available architecture
1. A route table is automatically provisioned when you create a VPC
1. You can create a route table, and assign it to a subnet
1. Each subnet can be associated with only 1 route table
### Internet Gateway
1. a gateway out to internet.
1. You can only have 1 internet gateway per VPC
1. Internet gateway needs to be attached to a subnet
1. EC2 do not automatically get connection to internet. You need to connect the E2 via Elastic Ip or Elastic load balancer
1. Steps to get internet
1. Create internet gateway
1. Attach internet gateway to vpc
1. create a new route table and attach it to a subnet
1. Edit route table and attach it to internet gateway
1. Create elastic ip or elb and attach it to ec2 created under the vpc
1. under aws, you can have 251 ip addresses, opposed to industry standard 254 as they reserve a few
1. EC2 launched under a dedicated subnet will not have a public DNS or a public IP The only way to get a public IP is by creating a gateway and : assigning IP addresses manually or using ELB groups
1. Even if you attach a public IP address , you still need a route to the internet to ssh in or for access over internet
1. You can ssh into one EC2 and then to the other EC2 without public address from within as they are all members of same subnet. So you can connect to public instance first and then to the internal instances from within the public instance
1. Each subnet can only be associated with one route table
1. Access Control Layer ACL
1. ACL allows to create firewall rules that deny or allow traffic at subnet / network level. This is tighter than security group
1. ACL are stateless filtering
1. Security group sits in front of EC2 instance and allow or deny traffic at EC2 level
1. NAT instance can make private machines inside vpc access internet, however the machines are not publically accesible
