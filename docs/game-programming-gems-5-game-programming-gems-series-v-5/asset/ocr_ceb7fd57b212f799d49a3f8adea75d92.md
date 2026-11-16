before the ancillary packet is routed to a PE, the linked packet is scheduled for execution. Linked packets should be used with care, as they are extremely susceptible to race conditions and deadlock issues that can also lead to thread leakage (discussed later).

While implementing a task scheduler is fairly straightforward, individual task selection mechanisms are highly game-specific. One key component is data processing. If the PEs are being starved (waiting for data), the AI routines that supply tasks to the pool need to take this into consideration. When starvation is observed, it is important to rework the AI routines and scheduling logic so that it is more anticipatory of potential processing holdups.

# Caching or Processor Affinity

Caching or processor affinity encourages similar tasks to be executed on processors that have executed identical or similar tasks, an important consideration when offloading tasks to PEs. To accommodate this processor affinity, the task manager should contain a basic history tracking system. The basic history tracking contains a list of differing tasks and the most recent processor element that executed it.

# Interruption

Once a task is routed off to a processor element for execution, it is critical that the task proceed uninterrupted. We allow any offloaded task to be completed before another task is routed to that processor element. This eliminates an entirely cumbersome mechanism of stalling processes, storing the entire state of a processor element, just because a higher priority task was entered into the task manager. If you find that a task needs to be interrupted, the task is most likely too large and needs to be broken down into smaller tasks.

A typical example from an RTS game is the generation of an influence map. A unit attacking a group of enemy tanks may not necessarily need the *entire* influence map regenerated, which can potentially become a bottleneck during normal gameplay due to the size of most influence maps. Instead, the creation of a *tactical influence map* can be used. A tactical influence map is just a smaller influence map that is focused on a particular region of interest. This allows all the normal operations of the larger influence map to occur, just on a finer scale. You don't have to limit the scope of your tasks; designing a smaller data set to work with will alleviate the possible task interruptions.

# Load Balancing

When creating a task for execution, we must consider the actual size of the workload that a PE will be expected to process. If the workload is too small, the PE will be starved for data, spending more time preparing and communicating then actually processing tasks. If the task is large and takes too long to execute, it may cause data dependency issues. Worse, it may delay the delivery of a crucial result to the game, such that a gap in the decision-making process becomes evident.