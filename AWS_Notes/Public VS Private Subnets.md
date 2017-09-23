If a machine **has a public IP**, it goes in a public subnet and uses the IGW as its default route.
If it **doesn't have a public IP**, it goes in a private subnet and uses a NAT instance as its default route.

If you have web servers without public addresses, behind an ELB... then the ELB itself goes in the public subnet, but the instances go in the private subnet.

The subnets where an ELB is provisioned have nothing to do with the subnets where the instances it is balancing are provisioned.



