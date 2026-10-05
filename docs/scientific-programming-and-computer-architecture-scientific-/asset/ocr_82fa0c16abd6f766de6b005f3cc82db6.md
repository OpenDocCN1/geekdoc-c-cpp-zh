230

Chapter 4. Memory

| 128-bit FPU | |
| Load/ store | L1 data cache | L2 cache |
| Execution | L2 ctl |
| Fetch/decode/branch | L1 instr cache |

Figure 4.5: Layout of a single core of AMD Opopter (code named Barcelona) (layout based on Patterson and Hennessy).

# 4.1.2 Cache memory

An instruction as movq %rax, %rdx, which moves one register to another, takes a single cycle. However, a load instruction as movq (%rsi), %rdx, which moves a quad word from memory to a register, can take more than 100 cycles. An instruction that writes can take even longer. Computer processors frequently used parts of DRAM memory so that they execute instructions at the speed of the registers, although nearly half the instructions are loads and stores from the much slower DRAM devices.^3

Figure 4.5 shows the layout of a single processor core. About half the area of the cache is taken up by cache memory and the memory controller. The latency to L1 cache memory is a 4 cycles. It is much faster to access cache than to access memory.

The basic principle of cache organization is data locality. Once a word is accessed

> ^3The classic by Hennessy and Patterson (1990-2011) has a thorough discussion of caches. There is a lot of information in the Intel manuals as well.