![](bbox=[0.335, 0.115, 0.665, 0.335])

FIGURE 10.8
Multi-GPU data pathways.

is clearly supporting. Generally, you find the size of a backer and the take up among programmers will largely dictate the success or failure of a given software programming initiative. Most standards, regardless of who develops them, largely cover the same space, so in most cases learning one makes it much easier to learn another.

If you are interested in writing GPU code using directives, you will likely already have a reasonable understanding of the OpenMP directives for CPUs. The major difference we find with standards such as OpenACC is that they, and thus the programmer, also have to deal with the location of data. In an OpenMP system where there is more than a single physical socket for the CPU we have what is called a NUMA (nonuniform memory access) system.

As we can see from Figure 10.8, memory in a system with more than one CPU is attached directly to a given CPU. Thus, a process that resides on CPU0 takes considerably longer to access memory that resides on CPU1 than if that memory was local to CPU0. Let's assume we have eight processes running over two CPU sockets, each CPU with four cores. To perform an exchange of data that requires many-to-many communications means we're limited to the throughput of the slowest communication link. This will be the QPI/hypertransport link between processors over which the memory traffic to the other processor's memory bus must go. The OpenMP model simply ignores this effect and lacks many of the data concepts accelerator-based solutions require.

# OpenACC

OpenACC is a move toward directive programming and very much follows in the footsteps of OpenMP, which has been very successful within standalone, single machines. OpenACC is aimed at:

+   - Independent loop-based parallelism.
+   - Programmers who have not yet been exposed to CUDA or found it too complex.