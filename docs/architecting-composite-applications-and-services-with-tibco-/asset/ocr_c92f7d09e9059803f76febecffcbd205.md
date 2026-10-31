![](bbox=[0.102, 0.115, 0.895, 0.485])

**Figure 16-16:** *EMS Multi-Site with No Message Persistence—Before Failover*

File-Based Intra-Site Failover Pattern, with the primary being deployed at one site and the secondary at the other site. A shared file system is not necessary, since there are no persisted messages. Synchronous file replication is used to maintain copies of each server’s configuration files at the other site.

Note that there are two file systems being replicated, and in opposite directions. The J File System’s primary is at the primary site, with a copy at the secondary site. The K File System’s primary is at the secondary site, with a copy at the secondary site. This allows for initial failover in either direction.

The situation after the primary EMS server has failed but before it is recovered at the secondary site is shown in Figure 16-17. If the EMS servers are configured with the default heartbeat settings (three-second heartbeats, a ten-second absence triggering failover), this state is reached in ten seconds, well below the five minutes required for 99.99% availability. However, the reliability of the inter-site network comes into play: A failure will result in an apparent loss of heartbeats from the secondary