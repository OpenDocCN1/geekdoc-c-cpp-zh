```
for(int i=0; i < 1000*1000*1000; i+=16)
    sum += a[i];
return sum;
```

In stride16(), the cost of accessing a single entry of the array is about 13 cycles, which is once again much smaller than the latency to DRAM. As many as 10 memory reads can be in flight at the same time. Strided accesses benefit from parallelism in the instruction pipeline and the memory system. Strided accesses are particularly easy to predict. It is likely that the prefetch engines in the memory controller are able to prefetch many of the locations accessed in stride16() into cache ahead of time. A more refined attempt follows.

```
// List must be 64 byte aligned
void accessList(long int *List, long int n, int count,
    double *x) {
    long int index = 0;
    for(int i=0; i < count; i++){
        x += List[index];
        index = List[index]%n;
        index = index %8;
    }
```

The loop defined in lines 5 through 9 works as follows. It reads the List[index] on lines 6 and 7, and the next entry is determined by the earlier entry on lines 7 and 8. It is assumed that all entries of List[] are initialized to non-negative. The next load instruction cannot be issued until the earlier load instruction is complete because the address of the next load instruction is determined by the result of the earlier load instruction. This way of accessing memory arrays breaks instruction-level parallelism.

The function accessList() is called with n=10^9 and count=6000. The array List is initialized with pseudorandom numbers. We verified explicitly (verification not shown here) that the 6000 entries accessed in the body of the loop were all distinct. Line 8 ensures that every index used to look up List[] is a multiple of 8. All transfers between DRAM memory and cache are done in cache lines. A single cache line is 64 bytes. The array List is assumed to be 64 byte aligned (the last