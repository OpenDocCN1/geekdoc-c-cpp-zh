![](bbox=[0.217, 0.116, 0.696, 0.327])

**Figure 16-14:** *ActiveMatrix BusinessWorks Cluster Failover—Before Failover*

The ActiveMatrix BusinessWorks engine retrieves its checkpoint files and resumes the execution of those jobs (Figure 16-15).

The use of cluster-style failover has some advantages over the built-in approach:

+   - The use of the file system as opposed to the database for storing checkpoints is faster.
+   - All the process starters will continue to work properly since the back-up instance of ActiveMatrix BusinessWorks is running in the same virtual environment.
+   - The same pattern can be used for both intra- and inter-site failover.

![](bbox=[0.212, 0.636, 0.701, 0.887])

**Figure 16-15:** *ActiveMatrix BusinessWorks Cluster Failover—After Failover*