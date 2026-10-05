all the capacities. By dividing that by the number of processors per group, the kernel assumes there will be this many total groups on the machine (limited to a maximum of 20). In group maximization, the initial estimate is that there will be as many groups as nodes (limited to 20).

+   7. The kernel begins the final assignment process. All fixed assignments from earlier are now committed and are created for those assignments.

+   8. All the NUMA nodes are reshuffled to minimize the distance between the different nodes within a group. In other words, closer nodes are part in the same group and sorted by distance.

+   9. The same process is performed for any dynamically configured node to group assignments.

+   10. Any remaining empty nodes are assigned to group 0.

# Logical processors per group

Generally, Windows assigns 64 processors per group. But you can also customize this configuration by using different options such as the /GROUPSIZE option, which is configured through the groupsize BCD element. By specifying a number that is a power of 2, you can force cores to contain fewer processors than normal for purposes such as testing group awareness in the system. For example, with system logical processors can be made to appear as one, two, or four groups. To force the issue, /FORCEGROUPWARE option (bcd element groupaware) causes the kernel to avoid group 0 whenever possible, assigning the highest number available in actions such as thread and DPC affinity selection and process group assignment. You should avoid setting group size of 1 because this will force all applications to behave as if they're running on a uniprocessor machine. This means the kernel sets the affinity mask of a given process to only one core unless the application requests otherwise (which applications will not)

Other than significant driver and application compatibility problems—which are designed to identify and root out, when went by developers—these options have an even greater impact on the machine: They force NUMA behav to span multiple groups, as shown in the assignment algorithms. If the kernel is creating artificially small groups, those groups must each have their own NUMA node. For example, on a quad-core processor with a group size of 2, this will create two groups, and two NUMA nodes, which will be subnodes of the main node. This will affect scheduling and memory-management policies in the same way as true NUMA system, which can be useful for testing.