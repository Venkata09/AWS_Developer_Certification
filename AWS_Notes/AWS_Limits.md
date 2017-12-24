### AWS services and the limits for the 

1. VPCs per region: 5
1. Subnets per VPC: 200
1. Route tables per VPC: 200 (including main route table)
1. Network ACLs per VPC: 200
1. Active VPC peering connections per VPC: 50
1. Outstanding VPC peering connection requests: 25
1. Internet Gateway per region: 5
1. Virtual private gateway (VGW) per region: 5
1. Customer Gateway (CGW) per region: 50
1. VPN connections per region: 50
1. Entries per route table: 50
1. EIP per region for each account: 5
1. Security groups per VPC: 100
1. Rules per security group: 50 (per network interface max limit: 250)
1. Security groups per network interface: 5
1. Rules per ACL: 20
1. BGP advertised routes per VPN Connection: 100


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


### SQS Related Timeout limits.

1. Messages in the Queue can be **retained** for up to 14 days. (How long can I keep my messages in Amazon SQS message queues) --> 1 minute to 14 days. By default it's 4 days.
1. Visibility timeout by default is 30 Seconds up to 12 hour maximum 
1. Maximum long polling timeout 20 seconds
1. SQS - Message can contain upto 256KB of text, billed at 64KB chunks,
1. Single request can have 1 to 10 messages unto maximum of 256KB payload
1. Even though there is one message of 256Kb its basically 4 request for billing since (4 * 64KB)

### CloudWatch
1. 1 minute data point are available for 15 days.
1. 5 minute data points are available for 63 days.
1. 1 hour data points are available for 455 days.

### RDS
1. How many reserved instances can I purchase? You can purchase up to **40 reserved DB instances**.
