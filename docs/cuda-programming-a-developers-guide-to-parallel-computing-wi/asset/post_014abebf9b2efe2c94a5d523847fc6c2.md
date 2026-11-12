
## Using CUDA in Practice

## INTRODUCTION

In this chapter we'll look at a few examples of the not-so-common uses of GPUs to provide insight into how to solve a number of different types of computer problems. We'll look at the problems involved in using GPUs for such computations.

## SERIAL AND PARALLEL CODE

### Design goals of CPUs and GPUs

CPUs and GPUs, although both execute programs, are a world apart in their design goals. CPUs use an MIMD (multiple instruction, multiple data) approach, while GPUs use an SIMT (single instruction, multiple thread) instruction model.

The CPU approach to parallelism is to execute multiple independent instruction streams. Within those instruction streams it seeks to extract instruction level parallelism. That is, it fills a very long pipeline of instructions and looks for instructions that can be sent to independent execution units. These execution units usually consist of one or more floating-point units, one or more integer units, a branch prediction unit, and one or more load/store units.

Branch prediction is something computer architects have worked extensively on for over a decade or so. The problem with branching is that the single instruction stream turns into two streams, the branch taken path and the branch not taken path. Programming constructs such as while loops typically branch backwards to the start of the loop until the loop completes. Thus, in a lot of cases, the branch can be predicted statically. Some compilers help with this in setting a bit within the branch instruction to say if the branch is likely to be met or not. Thus, loops that branch backwards can be predicated as taken, whereas conditionals are usually predicated as not taken, thus avoiding the branch altogether. This has the added advantage that the next instructions have typically already been pre-fetched into the cache.

Branch prediction evolved from the simple but quite effective static model, to use a dynamic model that records previous branching history. Multiple levels of complex branch prediction are actually present in modern processors due to the very high cost of a mispredicted branch and the consequential refilling of the long execution pipeline.

Along with branch prediction, a technique called speculative execution is used. Given the CPU will likely have predicted a branch correctly, it makes sense to start executing the instruction stream at that branch address. However, this adds to the cost of branch misprediction, as now the instruction stream that has been executed has to be undone or discarded.

The optimal model for both branch prediction and speculative execution is simply to execute both paths of the branch and then commit the results when the actual branch is known. As branches are often nested, in practice such an approach requires multiple levels of hardware and is therefore rarely used.

Finally, we have the other major difference, seen until recently, which is the amount and number of cache memory levels. The CPU programming model works on the nice principle of abstraction, that is, the programmer doesn't have to care where the memory is because the hardware takes care of it. For most programs, except those that need to run fast, this works quite well. It used to be that instruction cycles were expensive, but with ever-increasing chip density, instruction cycles are now cheap. Accessing memory is now the bottleneck on modern processor design and this is addressed by the multiple levels of cache.

GPUs, until the introduction of Fermi, took an alternative approach to this design. Fermi designers believe the programmer is best placed to make use of the high-speed memory that can be placed close to the processor, in this case, the shared memory on each SM. This is the same as the L1 cache found on a conventional processor, a small area of low latency and higher bandwidth memory. If you think about most programs, this makes a lot of sense. A programmer knows the program better than anyone else and therefore should be able to identify which off-chip memory accesses can be prevented by using shared memory.

Fermi expanded the on-chip memory space to 64K, 16K of which must be allocated to an L1 cache. So that there was always some shared memory present, they did not allow the entire space to be allocated to either cache or shared memory. By default, Fermi allocates 48K to shared memory and 16K to cache. However, you can switch this and have 48K of cache and 16K of shared memory. Kepler also introduces a 32K/32K split option. In programs that make no use of shared memory, setting this switch to prefer L1 cache instead of shared memory can significantly improve performance for memory-bound kernels. This is done with a call to

```
cudaFuncSetCacheConfig(cudaFuncCachePreferL1);
```

In the sample sort program we use to look at optimizing later in this chapter, this simple change reduced the overall execution time by 15%. This is a huge bonus for enabling a feature that is disabled by default.

With the inclusion of an L1 cache, GPUs and CPUs moved closer to one another in terms of the data fetched from memory. With previous GPU generations, memory accesses needed to be coalesced to achieve any sort of performance. Consider a noncoalesced memory fetch on the G80 and GT200 based hardware. If thread 0 reads from memory address 0x1000, thread 1 reads from 0x2000, thread 2 reads from 0x3000, etc., this results in one memory fetch per thread of 32 bytes. Not 32 bits, but 32 bytes, the minimum memory transaction size. The next access (0x1004, 0x2004, 0x3004, etc.) did exactly the same.

In Fermi, as with CPUs, a cache line of 128 bytes is fetched per memory access. Thus, subsequent access by an adjacent thread will usually hit the cache instead of having to go out to global memory on the device. This allows for a far more flexible programming model and is more akin to the CPU programming model most programmers are familiar with.

One of the aspects of GPU design that differs significantly from CPU design is the SIMT model of execution. In the MIMD model, there is separate hardware for each thread, allowing entirely separate instruction streams. In the case where the threads are processing the same instruction flow, but with different data, this approach is very wasteful of hardware resources. The GPU thus provides a single set of hardware to run N threads, where N is currently 32, the warp size.

This has a significant impact on GPU program design. SIMT implementation in the GPU is similar to the old vector architecture SIMD model. This was largely abandoned in the early 1970s when the ever-increasing speed of serial CPUs made the "hard" programming of SIMD machines less than appealing. SIMT solves one of the key issues, in that programmers are no longer forced to write code in which every SIMD follows the same execution path. Threads can diverge and then converge at some later point. The downside of this flexibility is that there is only one set of hardware to follow multiple divergent program paths. Thus, each path must be executed in turn, or serialized, until the control flow converges once more. As a programmer you must be aware of this and think about it in the design of your kernels.

Finally, we'll come to one other significant difference between CPUs and GPUs. On the CPU model, there is serial control flow. Executing an instruction that requires a number of cycles to complete will stall the current thread. This is one of the reasons why Intel uses hyperthreading. The hardware internally switches to another thread when the current one stalls. GPUs have not just one other thread, but are designed to have thousands of other threads that they can potentially switch to. Such a stall happens as a result of both instruction latency and memory latency, that is, where the processor is waiting on the completion of an operation. The threading model is designed to hide both.

However, the GPU has one other benefit in that it uses lazy evaluation. That is, it will not stall the current thread until there is an access to the dependent register. Thus, you may read a value into a register early in the kernel, and the thread will not stall until such time as (sometime later) the register is actually used. The CPU model stalls at a memory load or long latency instruction. Consider the following program segments.

### Segment 1:

```
int sum=0;
for (int i=0; i< 128; i++)
{
sum += src_array[i];
}
```

If we look at the first segment, the program must calculate the address of src_array[i], then load the data, and finally add it to the existing value of sum. Each operation is dependent on the previous operation.

### Segment 2:

```
int sum=0;
int sum1=0, sum2=0, sum3=0, sum4=0;
for (int i=0; i< 128; i+=4)
{
sum1 += src_array[i];
sum2 += src_array[i+1];
sum3 += src_array[i+2];
sum4 += src_array[i+3];
}
sum = sum1 + sum2 + sum3 + sum4;
```

If we look at the second segment, we iterate in steps of four. Four independent sum values are used, allowing four independent summations to be computed in the hardware. How many operations are
