If a machine **has a public IP**, it goes in a public subnet and uses the IGW as its default route.

If it **doesn't have a public IP**, it goes in a private subnet and uses a NAT instance as its default route.

If you have web servers without public addresses, behind an ELB... then the ELB itself goes in the public subnet, but the instances go in the private subnet.

The subnets where an ELB is provisioned have nothing to do with the subnets where the instances it is balancing are provisioned.



By using public IP addresses you have the benefit of being able to easily expose certain services to a limited audience without needing to use something like an ELB. This frees you from the need to set up a NAT instance or NAT gateway. And since you need half as many subnets, you could choose to use a smaller CIDR allocation for your VPC or you could make bigger subnets with the same size VPC. And fewer subnets means you'll be paying less for inter-AZ traffic as well.



**So, why don't we do this? Why does AWS say the best practice is to use private IPs?**

Amazon Web Services has a limited supply of public IPv4 addresses because the internet as a whole has a limited supply of public IPv4 addresses. It is in their best interest for you to use private IP addresses which are effectively unlimited, rather than excessively consuming scarce public IPv4 addresses. **You can see some evidence of this in how AWS prices Elastic IP's; an EIP attached to an instance is free, but an unused EIP costs money.**



There are only two ways to attach a public IP address to an EC2 instance in a VPC.

1. Associate Public IP Address

You can request a public IP address when launching a new EC2 instance. This option appears as a checkbox in the console, as the --associate-public-ip-address flag when using aws-cli, and as the AssociatePublicIpAddress flag on an embedded network interface object when using CloudFormation. In any case, the public IP address is assigned to eth0 (DeviceIndex=0). You can only use this approach when launching a new instance. However, this comes with some drawbacks.

One of the advantages of using EC2 instances in a VPC is that you can change the assigned security groups on the fly. But if you have opted to associate a public IP address, you lose that ability. It's actually even worse than that. If you're using CloudFormation and you change the security group of an instance that is using an embedded network interface object, that forces immediate replacement of the instance.

Another disadvantage is that a public IP address assigned in this way will be lost when the instance is stopped.

2. Elastic IP

In general Elastic IP's are the preferred approach because they are safer. You are guaranteed to continue using the same IP address, you don't risk accidentally deleting any EC2 instances, you can freely attach/detach an Elastic IP at any time, and you have the freedom to change security groups applied to your EC2 instances.

... But AWS limits you to 5 EIP's per region. You can request more, and your request might be granted. But AWS could just as likely deny that request based on the reasoning I mentioned above. So you probably don't want to rely on EIP's if you plan on ever scaling your infrastructure beyond 5 EC2 instances per region.

In conclusion, using public IP addresses does come with some nice benefits, but you'll run into administrative or scaling problems if you try to use public IP addresses exclusively. Hopefully this helps to illustrate and explain why the best practices are the way they are.






It is worth noting that the AWS managed gateway is ~3 times more expensive as on date when compared to running your own instance. 

Managed NAT instance monthly cost = $33.48/month ($0.045/hour * 744 hours in a month) + $4.50 ($0.045 per GB data processed * 100GB) + $10 ($.10/GB standard AWS data transfer charges for all data transferred via the NAT gateway) = $47.98

t2.nano instance configured as a NAT instance = $4.84/month ($0.0065 * 744 hours in a month) + $10 ($.10/GB standard AWS data transfer charges for all data transferred via the NAT instance) = $14.84








