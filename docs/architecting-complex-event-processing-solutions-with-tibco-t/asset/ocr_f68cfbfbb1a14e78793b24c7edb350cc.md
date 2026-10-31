If there are multiple objects that need to be locked, there is the possibility of a deadly embrace: X locks A and then tries to lock B, while Y has locked B and is attempting to lock A. Neither X or Y will be able to proceed. For this reason, it is important to specify the timeouts for the locks and provide appropriate exception handling.

The likelihood of a deadly embrace can be greatly reduced by following another programming convention: If you plan to lock multiple objects, then obtain all of their keys, sort the keys, and then obtain the locks in the sorted sequence.

Remember, the effectiveness of locks depends entirely upon the consistency of their use!

# Cache Object Replication

The cache can be configured to automatically replicate objects, with the copies of objects residing in different cache agents (Figure 6-6). There are two settings for this configuration. One is Number of Backup Copies, which determines the number of extra copies (in addition to the original) that will be maintained in the cache. The default is one. The other setting is Cache Agent Quorum, which determines the minimum number of cache agents that must be running before the cluster will begin operating. It doesn't make any sense to have back-up copies of objects if they are all present in the same cache agent, so this number should be at least one greater than the number of back-up copies. If you want to maintain replication even if a cache agent goes down, increase this number. This setting has no effect on operation once the cluster has started other than causing a log entry to be made if the actual number of running cache agents falls below this number.

![](bbox=[0.15, 0.78, 0.9, 0.92])

Figure 6-6: Configuring Cache Object Replication