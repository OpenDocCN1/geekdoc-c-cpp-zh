then the EMS server instance can be started. Depending upon the environment, this may take several minutes.

# Persisted Message Read Time

If there are persisted messages, the secondary server must read them before it can begin providing service. In doing this, reading from a file system will always be faster than reading from a database. The file-based read time can be further decreased by splitting the message storage among multiple files, which will be read concurrently.

# File Locking Reliability

From an RTO perspective, the winning strategy appears to be file-based failover—but only if a shared file system with reliable file locking is available. Don't get trapped into trying to make it work with NFS V2 or V3 (many a group has tried and failed), and if you're looking at NFS V4 you need to ensure that your operating system is configured to use the locking properly (which it won't be by default). An unreliable file-locking mechanism means an unreliable failover pattern.

# Administrative Complexity

From the perspective of administrative complexity, the generic failover approach is, by far, the winner. There is exactly one server configuration, and it can be used both for failover within a data center and between data centers. Client configurations remain the same as well. There is also the benefit of uniformity across different types of components: The management of the failover process is the same as for all components using cluster-style failover.

# ActiveMatrix BusinessWorks Failover

There are three major patterns that can be used to achieve high availability with ActiveMatrix BusinessWorks engines. These patterns are available whether BusinessWorks is running as a stand-alone engine or embedded in an ActiveMatrix node:

+   1. ActiveMatrix BusinessWorks Deferred JMS Acknowledgement Pattern
+   2. ActiveMatrix BusinessWorks Built-In Intra-Site Failover Pattern
+   3. ActiveMatrix BusinessWorks Cluster Failover Pattern