buy and set up a cluster. Sometimes they can simply be made from a number of old PCs that are being replaced, so the hardware is effectively free.

However, the problem with cluster computing is it's only as fast as the amount of internode communication that is necessary for the problem. If you have 32 nodes and the problem breaks down into 32 nice chunks and requires no internode communication, you have an application that is ideal for a cluster. If every data point takes data from every node, you have a terrible problem to put into a cluster.

Clusters are seen inside modern CPUs and GPUs. Look back at Figure 1.1. The CPU cache hierarchy. If we consider each CPU core as a node, the L2 cache as DRAM (Dynamic Random Access Memory), the L3 cache as the network switch, and the DRAM as mass storage, we have a cluster in miniature (Figure 1.6).

The architecture inside a modern GPU is really no different. You have a number of streaming multiprocessors (SMs) that are akin to CPU cores. These are connected to a shared memory/L1 cache. This is connected to an L2 cache that acts as an inter-SM switch. Data can be held in global memory storage where it's then extracted and used by the host, or sent via the PCI-E switch directly to the memory on another GPU. The PCI-E switch is many times faster than any network's interconnect.

The node may itself be replicated many times, as shown in Figure 1.7. This replication within a controlled environment forms a cluster. One evolution of the cluster designs are distributed

![](bbox=[0.11, 0.46, 0.87, 0.85])

**FIGURE 1.6**
Typical cluster layout.