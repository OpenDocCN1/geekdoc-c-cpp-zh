# Disaster and Recovery Planning

In a traditional IT environment, disaster planning involves creating system backups, creating a service restoration plan, managing an IT infrastructure to enable redundancy and availability, and colocating backups and valuable data in multiple locations. Cloud computing and virtualized solutions enable new approaches to durable and disaster-proof service but also pose new requirements in the implementation of these services, including replication across cloud regions, recovery plans that include multiple cloud providers, and backups on cloud-based storage systems. Reese (2009, 119) discusses a range of issues related to disaster recovery in the cloud including data backups, server configuration storage, server redundancy, and disaster monitoring. Velte et al. (2009, 37) mention several benefits of using the cloud for backup including reduced data loss, simplified monitoring, faster recovery, and improved security.

Whatever the benefits, a cloud-based backup, replication, and recovery strategy needs to be considered within the context of organizational risk tolerance and legal liability. For example, when organizations shift away from local IT infrastructure to cloud platforms there is an increased need to support service replication across multiple cloud providers, backup data on multiple cloud networks, and automate processes to ensure that the library can leverage the backup, replication, and scalability features typically associated with cloud platforms. Cloud computing is still a relatively new technology and, though rare, cloud providers periodically

# Issues to Consider for Service Durability

Regardless of platform or type of service, consider the following issues when adopting a cloud platform:

+   - Database backup and restoration procedures.
+   - Replicated storage of long-term digital resources.
+   - Documentation of server configuration and service interactions. In an optimal situation, this would be implemented using an automatic configuration system (see chapter 5).
+   - Automatic redundancy of cloud services within a cloud provider. A key method of avoiding downtime is to implement services that feature continuous data protection, automatic scaling, and multizone replication of services.