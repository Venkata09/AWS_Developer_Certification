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


### SQS Related Timeout limits.

1. Messages in the Queue can be retained for up to 14 days
1. Visibility timeout by default is 30 Seconds up to 12 hour maximum 
1. Maximum long polling timeout 20 seconds
1. SQS - Message can contain upto 256KB of text, billed at 64KB chunks,
1. Single request can have 1 to 10 messages unto maximum of 256KB payload
1. Even though there is one message of 256Kb its basically 4 request for billing since (4 * 64KB)
