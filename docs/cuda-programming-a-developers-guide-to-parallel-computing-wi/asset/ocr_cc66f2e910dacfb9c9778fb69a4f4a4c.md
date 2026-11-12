This has a significant impact on GPU program design. SIMT implementation in the GPU is similar to the old vector architecture SIMD model. This was largely abandoned in the early 1970s when the ever-increasing speed of serial CPUs made the “hard” programming of SIMD machines less than appealing. SIMT solves one of the key issues, in that programmers are no longer forced to write code in which every SIMD follows the same execution path. Threads can diverge and then converge at some later point. The downside of this flexibility is that there is only one set of hardware to follow multiple divergent program paths. Thus, each path must be executed in turn, or serialized, until the control flow converges once more. As a programmer you must be aware of this and think about it in the design of your kernels.

Finally, we’ll come to one other significant difference between CPUs and GPUs. On the CPU model, there is serial control flow. Executing an instruction that requires a number of cycles to complete will stall the current thread. This is one of the reasons why Intel uses hyperthreading. The hardware internally switches to another thread when the current one stalls. GPUs have not just one other thread, but are designed to have thousands of other threads that they can potentially switch to. Such a stall happens as a result of both instruction latency and memory latency, that is, where the processor is waiting on the completion of an operation. The threading model is designed to hide both.

However, the GPU has one other benefit in that it uses lazy evaluation. That is, it will not stall the current thread until there is an access to the dependent register. Thus, you may read a value into a register early in the kernel, and the thread will not stall until such time as (sometime later) the register is actually used. The CPU model stalls at a memory load or long latency instruction. Consider the following program segments.

# Segment 1:

```
int sum=0;
for (int i=0; i< 128; i++)
{
sum += src_array[i];
}
```

If we look at the first segment, the program must calculate the address of src_array[i], then load the data, and finally add it to the existing value of sum. Each operation is dependent on the previous operation.

# Segment 2:

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