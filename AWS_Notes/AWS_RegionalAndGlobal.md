AWS Global, Regional, AZ resource Availability


AWS provides a lot of services and these services are either Global, Regional or specific to the Availability Zone and cannot be accessed outside. 

AMIs – Regional

AMI provides templates to launch EC2 instances.
AMI is tied to the **Region** where its files are located with Amazon S3. For using AMI in different regions, the AMI can be copied to other regions

Auto Scaling - is **REGIONAL** spans across multiple Availability Zones within the same region but cannot span across regions

Elastic Load Balancer – Regional
Elastic Load Balancer distributes traffic across instances in multiple Availability Zones in the same region

Placement Groups – Availability Zone
Placement groups can be span across Instances within the same Availability Zones


S3 – Global but Data is Regional
S3 buckets are created within the selected region
Objects stored are replicated across Availability Zones to provide high durability but are not cross region replicated unless done explicitly
