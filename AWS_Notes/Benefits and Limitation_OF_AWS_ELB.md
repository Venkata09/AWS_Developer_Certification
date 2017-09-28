Key Benefits:

1. Distribution of requests to Amazon EC2 instances (servers) in multiple Availability Zones
1. Continuous monitoring of the health of Amazon EC2 instances registered with the load balancer so that requests are sent only to the healthy instances.
1. Support for end-to-end traffic encryption on those networks that use secure (HTTPS/SSL) connections.
1. The ability to take over the encryption and decryption work from the Amazon EC2 instances, and manage it centrally on the load balancer.
1. Support for the sticky session feature, which is the ability to "stick" user sessions to specific Amazon EC2 instances.
1. Association of the load balancer with your domain name. Because the load balancer is the only computer that is exposed to the Internet, you don’t have to create and manage public domain names for the instances that the load balancer manages. You can point the instance's domain records at the load balancer instead and scale as needed (either adding or removing capacity) without having to update the records with each scaling activity.
1. When used in an Amazon Virtual Private Cloud (Amazon VPC), support for creation and management of security groups associated with your load balancer to provide additional networking and security options.
1. Supports use of both the Internet Protocol version 4 (IPv4) and Internet Protocol version 6 (IPv6).
 

Key Limitation:

1. Major limitation is that it cannot provide permanent/Fixed IP Address for its load balancer. AWS generally recommend using CNAME rather A record.
1. You cannot put any redirection rule into it. Also does not support load balancing based on URL pattern.
1. Cannot have multiple web-pool behind a single end point.
1. Additional Options for Load Balancing Policies like weighted Round Robin, Least connection etc  is not in place.
1. Does not allow Load Balance to non-AWS End Points.
1. Some ISP’s do not allow Amazon ELB CNAMES that exceed 32 characters and some firewall versions/models (like Cisco PIX) will not allow larger CNAMES. In such cases try to have shorter names.
1. Amazon ELB currently timeouts persistent socket connections @ 60 seconds if it is kept idle. This condition will be a problem for use cases which generate large files (PDF, reports) at back end EC2, send them as response back and keep connections idle during the entire generation process.
1. Amazon ELB sticks request when traffic is generated from Single IP - This point comes as a surprise to many users using Amazon ELB. Amazon ELB behaves a little strangely when incoming traffic is originated from Single or Specific IP ranges, it does not efficiently complete the round robin and sticks the request.
1. Amazon ELB can only load balance the traffic, it does not have any caching mechanism to act as a web accelerator.
 
