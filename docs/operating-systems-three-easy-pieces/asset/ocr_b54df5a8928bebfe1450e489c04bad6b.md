# 38.9 Other Interesting RAID Issues

There are a number of other interesting ideas that one could (and per-haps) discuss when thinking about RAID. Here are some things we might eventually write about.

For example, there are many other RAID designs, including Levels 2 and 3 from the original taxonomy, and Level 6 to tolerate multiple disk faults [C+04]. There is also what the RAID does when a disk fails; some techniques have a hot sitting around to fill in the failed disk. What happens to performance under failure, and performance during recon-ruction of the failed disk? There are also more realistic fault models, to take into account latent sector errors or block corruption [B+08], and lots of techniques to handle such faults (see the data integrity chapter for details). Finally, you can build RAID as a software layer: such soft-ware systems are cheaper but have other problems, including the consistent-update problem [DAA05].

# 38.10 Summary

We have discussed RAID. RAID transforms a number of independent disks into a large, more capacious, and more reliable single entity; import-tantly, it does so transparently, and thus hardware and software are relatively oblivious to the change.

There are many possible RAID levels to choose from, and the exact RAID level to use depends heavily on what is important to the end-user. For example, mirrored RAID is simple, reliable, and generally provides good performance but at a high capacity cost. RAID-5, in contrast, is reliable from a capacity standpoint, but performs poorly when there are small writes in the workload. Picking a RAID and setting its parameters (chunk size, number of disks, etc.) properly for a particular workload is challenging, and remains more of an art than a science.