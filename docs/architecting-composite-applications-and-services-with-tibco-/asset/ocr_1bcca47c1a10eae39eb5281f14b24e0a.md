![](bbox=[0.12, 0.1, 0.88, 0.62])

Figure 16-17: EMS Multi-Site with No Message Persistence—During Failover

server taking over when the primary is still operational. Message delivery behavior under these circumstances is undefined.

The failure of the primary server also triggers the Site Failover with Same Host Identity Pattern, which causes the primary EMS server to be resurrected at the secondary site. After this failover is completed, you have the situation shown in Figure 16-18. The fault-tolerant pair of EMS servers has been restored, now both at the same site. Note, however, that the synchronous file replication of the primary’s configuration files (J File System) has been terminated. Restoration of the primary EMS server to the primary site will require additional design work.

# EMS Multi-Site with Message Persistence Pattern

This pattern is a combination of three patterns discussed earlier:

+   - EMS File-Based Intra-Site Failover Pattern
+   - Inter-Site Failover with Same Host Identity Pattern
+   - EMS Client Load Distribution: Queue Pattern (from Chapter 11)