updates that are then applied to the remote site. EMC, for example, provides this in the SRDF with Asynchronous option (SRDF/A). Remote updates are applied after the local component has been told the data has been successfully stored. Since there may be data in transit, this approach runs the risk of some data loss. For the updates managed in this manner by the storage subsystem, the RPO is generally in the range of seconds to a few minutes—but it is never zero.

Other asynchronous replication patterns involve taking snapshots of disks or performing tape backups. For these strategies to be appropriate, the RPO must be greater than the time interval between backups.

The sections that follow focus on design patterns involving synchronous file replication, since these are the most challenging. There are obvious variants of these patterns when asynchronous storage replication is used.

# Inter-Site Failover with Different Host Identity Pattern

The most complicated site failover patterns arise when the component is resurrected on a machine with a different host identity (Figure 16-5). With this pattern it is necessary to distinguish between data files used by the component and configuration files that define the component. The reason for this is that some of the configuration files contain information about the host identity. These files must be different at the two sites. Similarly, the configuration files for other components that access this component may also require configuration files that are different at the two sites.

During normal operation, the storage subsystem synchronously replicates the changes to the data file to the remote site. It does not, however, do anything with the configuration files. These must be manually placed and managed on the remote site and edited to reflect differences between the host environments.

Figure 16-6 shows the configuration after an inter-site failover has occurred. The recovered component is now running on the B machine using the configuration files that were specifically created for operation on that machine. It is using the synchronously replicated copy of the data from the primary site, so no data is lost.

Note that in this configuration, there is no data replication from the secondary site back to the primary site. After the primary site is restored, data from the secondary site must be replicated back to the primary site. This will likely require a fail-back scenario using asynchronous replication since, as of this writing, the author was unaware of any