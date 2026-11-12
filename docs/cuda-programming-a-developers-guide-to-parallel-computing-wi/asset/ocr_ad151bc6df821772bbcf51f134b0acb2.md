point per core, per iteration. GPUs run in parallel by default. Thus, instead of calculating just a single data point per SM, GPUs calculate 32 per SM. This gives a 4 times advantage in terms of number of cores (SMs) over a typical quad core CPU, but also a 32 times advantage in terms of data throughput. Of course, CPU programs can also use all the available cores and extensions like MMX, SSE, and AVX. The question is how many CPU applications actually use these types of extensions.

GPUs also provide something quite unique—high-speed memory next to the SM, so-called shared memory. In many respects this implements the design philosophy of the Connection Machine and the Cell processor, in that it provides local workspace for the device outside of the standard register file. Thus, the programmer can leave data in this memory, safe in the knowledge the hardware will not evict it behind his or her back. It is also the primary mechanism communication between threads.

# Task execution model

There are two major differences in the task execution model. The first is that groups of N SPs execute in a lock-step basis (Figure 5.3), running the same program but on different data. The second is that, because of this huge register file, switching threads has effectively zero overhead. Thus, the GPU can support a very large number of threads and is designed in this way.

Now what exactly do we mean by lock-step basis? Each instruction in the instruction queue is dispatched to every SP within an SM. Remember each SM can be thought of as single processor with N cores (SPs) embedded within it.

A conventional CPU will fetch a separate instruction stream for each CPU core. The GPU SPMD model used here allows an instruction fetch for N logical execution units, meaning you have 1/N the instructions memory bandwidth requirements of a conventional processor. This is a very similar approach to the vector or SIMD processors found in many high-end supercomputers.

However, this is not without its costs. As you will see later, if the program does not follow a nice neat execution flow where all N threads follow the same control path, for each branch, you will require additional execution cycles.

![](bbox=[0.24, 0.65, 0.75, 0.84])

FIGURE 5.3 Lock-step instruction dispatch.