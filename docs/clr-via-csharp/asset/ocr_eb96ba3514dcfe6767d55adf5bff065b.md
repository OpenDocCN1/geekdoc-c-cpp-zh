it designed the system to handle up to 64 CPUs in a single machine. At the time, 64 CPUs seemed like a lot, but today it looks like machines are going to get even more CPUs in them in the not-so-far-off future.

Starting with Windows Server 2008 R2, Microsoft has designed Windows to support machines that have up to 256 logical processors in them. Figure 25-4 shows how Windows supports all these logical processors. Here’s how to interpret the figure:

+   - A single machine has 1 or more processor groups where each group contains 1 to 64 logical processors.
+   - A processor group has one or more NUMA nodes. Each node contains some logical processors, cache memory, and local memory (all in proximity to each other).
+   - Each NUMA node has one or more sockets on it for silicon chips.
+   - Each socket’s chip contains one or more CPU cores.
+   - Each core contains one or more logical processors. There can be more than one logical processor if the chip is hyperthreaded.

![](bbox=[0.152, 0.429, 0.77, 0.913])

**FIGURE 25-4** Windows uses processor groups to support machines with up to 256 logical processors in them