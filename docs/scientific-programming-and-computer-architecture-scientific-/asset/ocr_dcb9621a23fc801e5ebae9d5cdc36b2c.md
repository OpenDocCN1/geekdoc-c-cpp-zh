238

Chapter 4. Memory

memory can differ from the latency of reading for certain types of DRAM. We limit ourselves to read latency for simplicity.

Measuring the latency to DRAM memory is a more complicated matter than one may realize at first sight. Many techniques are used to hide the latency to DRAM memory. Among these, the two most important are instruction-level parallelism and caching. Instruction-level parallelism enables the processor to issue a sequence of load or instructions to set up a pipeline of memory. If the pipeline can hold 10 memory accesses in various stages, the effective latency of a long stream of DRAM accesses is cut to a tenth. For example, the latency to DRAM is 200 cycles, the nth memory access may be initiated during cycle number 20n and completed during cycle number 20n+199. This sort of overlapping is possible only if the memory accesses are independent and there is sufficient parallelism in the instruction stream. Caching greatly reduces the effective latency of DRAM memory access as well. These techniques for hiding latency to memory are so effective that many programs do not realize how large the latency to DRAM memory can be.

Here is a first and not very careful attempt at measuring:

```
int unitstride(int *a){
    int sum=0;
    for(int i=0; i < 1000*1000*1000; i++)
        sum += a[i];
    return sum;
}
```

The function unitstride() loads 10^9 entries of a[] and computes their sum. The compiler unfolds the loop and introduces parallelism in the loop body. As a result, the running time of this function is determined by instructions that load entries of a[] and not by arithmetic.

The function unitstride() is timed as follows:

```
void time_unitstride(){
    int a[1000*1000*1000];
    a[0] = 0;
    for(int i=0; i < 1000*1000*1000; i++)
        Timestamp clk;
        clk.tick();
    unitstride(a);
```