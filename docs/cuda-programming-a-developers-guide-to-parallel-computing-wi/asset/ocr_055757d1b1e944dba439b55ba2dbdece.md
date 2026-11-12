![](bbox=[0.13, 0.105, 0.88, 0.165])

# FIGURE 6.5
Shared memory-based decomposition.

![](bbox=[0.13, 0.24, 0.88, 0.385])

# FIGURE 6.6
Shared memory bank access.

to the column without worrying about shared memory conflicts. The only thing you need to consider is branch divergence. You need to try to ensure that every thread follows the same execution flow, even though they are processing quite different data elements.

One side effect of this strategy is we will end up having to make a tradeoff. Assuming we have a single warp per SM, we will have no shared memory bank conflicts. However, a single warp per SM will not hide the latency of global memory reads and writes. At least for the memory fetch and write-back stage, we need lots of threads. However, during the sort phase, multiple warps may conflict with one another. A single warp would not have any bank conflicts, yet this would not hide the instruction execution latency. So in practice, we'll need multiple warps in all phases of the sort.

# Radix sort

One algorithm that has a fixed number of iterations and a consistent execution flow is the radix sort. It works by sorting based on the least significant bit and then working up to the most significant bit. With a 32-bit integer, using a single radix bit, you will have 32 iterations of the sort, no matter how large the dataset. Let's consider an example with the following dataset:

```
[ 122, 10, 2, 1, 2, 22, 12, 9 ]
```

The binary representation of each of these would be

```
122 = 01111010
10 = 00001010
2 = 00000010
22 = 00010110
12 = 00001100
9 = 00001001
```