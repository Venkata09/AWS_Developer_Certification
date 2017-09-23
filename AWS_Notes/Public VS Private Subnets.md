If a machine **has a public IP**, it goes in a public subnet and uses the IGW as its default route.

If it **doesn't have a public IP**, it goes in a private subnet and uses a NAT instance as its default route.

If you have web servers without public addresses, behind an ELB... then the ELB itself goes in the public subnet, but the instances go in the private subnet.

The subnets where an ELB is provisioned have nothing to do with the subnets where the instances it is balancing are provisioned.



By using public IP addresses you have the benefit of being able to easily expose certain services to a limited audience without needing to use something like an ELB. This frees you from the need to set up a NAT instance or NAT gateway. And since you need half as many subnets, you could choose to use a smaller CIDR allocation for your VPC or you could make bigger subnets with the same size VPC. And fewer subnets means you'll be paying less for inter-AZ traffic as well.



**So, why don't we do this? Why does AWS say the best practice is to use private IPs?**

Amazon Web Services has a limited supply of public IPv4 addresses because the internet as a whole has a limited supply of public IPv4 addresses. It is in their best interest for you to use private IP addresses which are effectively unlimited, rather than excessively consuming scarce public IPv4 addresses. **You can see some evidence of this in how AWS prices Elastic IP's; an EIP attached to an instance is free, but an unused EIP costs money.**



There are only two ways to attach a public IP address to an EC2 instance in a VPC.

1. Associate Public IP Address
1. Elastic IP




