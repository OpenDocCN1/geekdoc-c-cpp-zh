Each SM has a set of 32-bit registers stored in a register file that are partitioned among threads, and a fixed amount of shared memory that is partitioned among thread blocks. The number of thread blocks and warps that can simultaneously reside on an SM for a given kernel depends on the number of registers and amount of shared memory available on the SM and required by the kernel.

Figure 3-13 illustrates that when thread consumes more registers, fewer warps can be placed on an SM. If you can reduce the number of registers a kernel consumes, more warps will be processed simultaneously. Figure 3-14 illustrates that when a thread block consumes more shared memory, fewer thread blocks are processed simultaneously by an SM. If you can reduce the amount of shared memory used by each thread block, then more thread blocks can be processed simultaneously.

![](bbox=[0.095, 0.305, 0.78, 0.505])

FIGURE 3-13

![](bbox=[0.095, 0.545, 0.78, 0.765])

FIGURE 3-14

Resource availability generally limits the number of resident thread blocks per SM. The number of registers and the amount of shared memory per SM vary for devices of different compute capability. If there are insufficient registers or shared memory on each SM to process at least one block, the kernel launch will fail. Some of the key limits are shown in Table 3-2.