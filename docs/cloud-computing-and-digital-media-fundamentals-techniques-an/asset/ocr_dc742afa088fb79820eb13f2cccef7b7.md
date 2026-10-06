# GPU and Cloud Computing for Music Information Retrieval ■ 85

The following sections of this chapter describe our systems for QBSH and QBEE, and explain their deployment over a GPU-enabled cloud computing system.

#  4.2 BASICS OF GPU

The use of a GPU architecture can significantly accelerate both QBSH and QBEE for commercial or real-time applications. In this section, we briefly introduce the basics of GPU, using NVIDIA's GPU as an example.

As shown in Figure 4.3, GPU consists of several streaming multiprocessors (SMs), each composed of dozens of cores [streaming processors (SPs)], on-chip shared memories, and registers. The shared memory on each SM is usually 48 KB with 65,536 registers, with exact numbers depending on the type of GPU. It also features constant memory, texture memory, and global memory, which are shared by all of the SMs. Constant and texture memories can be accessed rapidly, but they are read-only by the GPU, and data can only be written to these memories by the central processing

![](bbox=[0.203, 0.497, 0.793, 0.881])

FIGURE 4.3 Basic GPU architecture.