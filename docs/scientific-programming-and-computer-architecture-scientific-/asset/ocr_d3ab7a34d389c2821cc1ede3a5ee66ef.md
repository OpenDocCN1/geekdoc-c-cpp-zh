# 3.3. Optimizing for the instruction pipeline

pipeline. As evident from figures 3.4 and 3.5, the stages within a pipeline are not linearly laid out, contrary to the image conjured by the word “pipeline,” but have more complicated interconnections with each other.

The SSE2 pipeline shown in figure 3.4 is for the Nehalem/Westmere architecture. The AVX2 pipeline shown in figure 3.5 is for the Haswell microarchitecture. The front-end, the reorder engine, and the execution units can differ when the instruction set is the same. However, such differences in microarchitecture are not always of the greatest significance for program optimization, although they could be on occasion.

# 3.3.2 Chipsets

So far have mainly been looking at the processor core. We are about to go even more deeply into the processor. Let us pause for a moment and look at the rest of the computer.

The processors are central to the computer but are only one among the components that make up a computer or computer node. Some of the other components are DRAM memory, graphics processor, hard disk, solid storage, network adapter, keyboard, and monitor. To understand how the processor is connected to all the components, we have to look at chipsets. Chipsets are used to assemble computers from many components.

Figure 3.6 shows the block diagram of the Intel 5500P chipset and gives a good idea of the layout of a computer. We pick a particular chipset, but many would just do as well at the level of generality of our discussion. The basic problem in assembling a computer is that the various components operate at very different speeds. The processors are very fast, DRAM memory is not so, peripherals such as keyboards are very slow, and the network is capricious. The task of reconciling components that operate at very different speeds falls partly on the chipset.

Two processor packages are shown in figure 3.6 as P1 and P2. Each processor package fits into a socket on the motherboard. Each processor package may have four or six cores in this instance. On more recent machines using other chipsets, each processor package may have 16 cores.

From figure 3.6, we see that DDR3 memory is connected to the sockets housing the processor. The processor packages contain multiple levels of cache and memory controllers to handle transfer of data to and from the DRAM channels. It is obvious from visual inspection that some DRAM memory channels are closer to