### EC2

AMI can be copied, and they can also be shared across multiple AWS accounts

AMI can also be copied from one availability region to another

EBS backed or instance storage. EBS can be attached or detached to an instance- Instance storage is ephemeral, data is lost when instance is terminated

spot instances Let you bid on unused instances. Amazon can take the spot instances away anytime

on demand instance

EC2- classic limits: 20 instances per account; 5 Elastic IP addresses. These can be increased by contacting AWS

EC2 uses ECC memories

Differences in instances: memory, compute power, block storage, network performance and EBS optimization

If instance is off state, then you only pay for data storage

When EC2-Classic is created, an IP address is assigned. This IP address can change when you start or stop the instance

When EC2-Classic is created, an CNAME is assigned. This CNAME can change when you start or stop the instance

You can setup an elastic IP address to maintain your IP address. This can be attached/detached to EC2

EC2-Clasic is deprecated

Termination protection can be used to avoid accidental termination

Default SDK region is US-EAST-1

Different storages:

s3, instance storage volume and EBS (/dev/sda1) : EBS are network attached storage
instance storage is instance attached storage
EBS can be attached only to 1 instance
volumes do not need to be un-mouted to take snapshots
atleast 1GB, and max of 1TB of EBS
EBS RAID 0 for redundancy
prewarming EBS: when EBS is reattached to EC2, EBS is erased on first mount causing loss of 5 to 50% OPS firs time. Prewarming can be used to avoid this.
EBS snapshots can be taken, they can be incremental
Availability zones are physically separate and do not share generators, coolers etc .

reserved instances: pay upfront to get guranteed compute

reserved instances cannot be moved to another region

reserved instances can be modified: move to another availability zone, convert the type of instance to larger or smaller size within same family ex convert 8 m1.small to 4 m1.medium etc ..

ELB allows to distribute traffic to available instances. Automatically stops traffic to unhealthy instance.

SSL certificates can be setup on ELB.

Maintaining session state when using ELB

session will be saved on individual instance. But if there are multiple instances load balanced, then session can be lost

Enable ELB cookie stickiness or application generated stickyness
Database or memcache can be used to solve the session problem as well in case of elasticache
Elasticache with memcache is the recommended way to sovle the cookie prolem.
When using elasticache, ELB works truly like ELB and not route all traffic to few instances based on cookies
