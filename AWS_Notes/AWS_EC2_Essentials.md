
 EC2 Bootstrapping, User-Data and Meta-Data

Viewing User-Data & Instance Meta-Data:
When logged into an EC2 instance, you can view the instance user-data used during creation, or meta-data, by executing one of the following commands:
curl http://169.254.169.254/latest/user-data  (displays bootstrapping commands)
curl http:// 169.254.169.254/latest/meta-data (displays AMI, instance type, etc)

Quiz

Q: IOPS are measured in what size “chunks?”
A: IOPS are measured in chunks of 256KB or smaller

Q: What best describes how EBS snapshots work?
A: Snapshots are incremental in nature and are stored in S3

Q: You are a Solutions Architect and your company is interested in moving some workload to AWS.  You are concerned that it will be very challenging to manage and control all of the EC2 servers that will need to be deployed – specifically, how to insure that fellow employees are installing the company approved operating system version, with the right libraries and runtimes and with the proper configuration settings.  What EC2 feature will best allow you to control this?
A: You can have a company policy stipulating that any new instance must be launched using a custom Amazon Machine Image (AMI) which specifies exactly which software and associated settings you want to have installed on every new EC2 instance.

T: AMIs are what dictate the instances operating system and other software settings. It is the "instance type" which determines the instances virtual hardware.

Q: What best describes the characteristics of EBS volumes?
A: They are persistent and can live past the lifetime of the instance.

Q: If you are running a legacy application that has hard-coded static IP addresses and is running on an EC2 instance, what is the best failover solution that allows you to keep the same IP address on a new instance?
A: Elastic IP addresses (EIPs) are designed to be attached/detached and moved from one EC2 instance to another. They are a great solution for keeping a static IP address and moving it to a new instance if the current instance fails. This will reduce or eliminate any downtime users may experience.

Q: If you are running an application in a production environment and must add a new EBS volume with data from a snapshot, what should you do to avoid degraded performance during the volume's first use?
A: Initialize the data by readying each storage block on the volume
E: Volumes created from an EBS snapshot must be initialized. Initializing occurs the first time a storage block on the volume is read, and the performance impact can be impacted by up to 50%. You can avoid this impact in production environments by manually reading all the blocks.

Q: What command should you run if you want to view an instance's user-data?
A: curl http://169.254.169.254/latest/user-data

Q: Your company has been thinking about moving its networking resources over to AWS. Your boss is particularly interested in the AWS shared responsibility model, as it will allow him to offload some traditional responsibilities to AWS. He says that he is happy that AWS will now handle the following responsibilities listed below. However, you know that he is wrong and that AWS does not handle all of them as part of the shared responsibility model. Which ... are not handled by AWS?
A1: Security Groups
A2: Applying an SSL Certificate to an ELB
A3: Installation of custom firewall software
E: In the shared responsibility model, AWS is responsible for DDOS protection, port scanning protection, and ingress network filtering. You are responsible for managing Security Groups, Applying an SSL Certificate to an ELB, and Installation of custom firewall software.

T: A key pair is a combination of a public and private key that is used for authenticating users when logging into an EC2 instance.
E: The public key pair is stored on the instance, and the private key is given to you when the instance is created.

Q: If you are designing an application that requires fast (10Gbps), low-latency connections between EC2 instances, what EC2 feature should you use?
A: Placement groups
E: Placement groups are a clustering of EC2 instances in one Availability Zone with fast (10Gbps) connections between them. This service is used for applications that need extremely low-latency connections between instances.

Q: You work in the IT department of a Fortune 500 financial services company. Your company has hundreds of servers and also uses VMware for certain applications. You happened to run into one of the senior directors in the hallway today, and she told you that she had just read an article on cloud computing that mentioned EC2 instances and was wondering what that was. What would be the best analogy to use in explaining to her what EC2 is?
A: EC2 is analogous to our internal VMware environment and provides companies with virtual servers that run in the cloud.

Q: What happens to data stored on an instance store volume when an EC2 instance is stopped or shutdown?
A: The data will be deleted
E: Since instance store volumes are ephemeral, data will NOT be persistent and WILL be deleted if the instance is stopped or shut down.



