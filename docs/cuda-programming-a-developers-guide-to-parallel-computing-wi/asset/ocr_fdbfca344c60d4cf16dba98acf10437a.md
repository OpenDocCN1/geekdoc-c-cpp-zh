# Multi-CPU and Multi-GPU Solutions

# INTRODUCTION

In modern computing systems it's common to have multiple devices, both CPUs and GPUs. In terms of CPUs we'll talk about sockets and cores. A socket is a physical socket on the motherboard into which a CPU is placed. A CPU may contain one or more cores. Each core is effectively a separate entity. A number of CPU and GPU sockets are located on a single node or computer system. Knowing the physical arrangement of cores, sockets, and nodes allows for far more effective scheduling or distribution of tasks.

# LOCALITY

The principle of locality is seen quite well in GPUs and CPUs. Memory closer to the device (shared memory on the GPU, cache on the CPU) is quicker to access. Communication within a socket (i.e., between cores) is much quicker than communication to another core in a different socket. Communication to a core on another node is at least an order of magnitude slower than within the node.

Clearly, having software that is aware of this can make a huge difference to the overall performance of any system. Such socket-aware software can split data along the lines of the hardware layout, ensuring one core is working on a consistent dataset and cores that need to cooperate are within the same socket or node.

# MULTI-CPU SYSTEMS

The most common multi-CPU system people will encounter is the single-socket, multicore desktop. Almost any PC you buy today will have a multicore CPU. Even in laptops and media PCs, you will find multicore CPUs. If we look at Steam's regular hardware (consumer/gaming) survey, it reveals that as of mid 2012 approximately 50% of users had dual-core systems and an additional 40% had quad-core or higher systems.

The second type of multi-CPU systems you encounter is in workstations and low-end servers. These are often dual-socket machines, typically powered by multicore Xeon or Opteron CPUs.