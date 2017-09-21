RDS - Regions & Availability Zones

A region consists of the multiple distinct locations called availabity zones. Each availabity zone is independent to itself interms of failures. AZ tries to provide inexpensive, low-latency network connectivity to other AZ's in the same region.

You can run your DB instance in several Availability Zones, an option called a Multi-AZ deployment. If you select this option, Amazon automatically **provisions and maintains a synchronous standby replica of your DB instance** in a different Availability Zone. The primary DB instance is synchronously replicated across Availability Zones to the standby replica to provide data redundancy, failover support, eliminate I/O freezes, and minimize latency spikes during system backups.
