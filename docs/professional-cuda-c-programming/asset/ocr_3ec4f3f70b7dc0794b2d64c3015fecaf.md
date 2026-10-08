approach is illustrated in Figure 6-7. As all streams are multiplexed into a single hardware work queue, the preceding streams block successive streams.

![](bbox=[0.115, 0.149, 0.842, 0.345])

FIGURE 6-6

To avoid dependencies on Fermi GPUs, you can dispatch job with breadth first in a breadth-first approach:

```
// dispatch job with breadth first way
for (int i = 0; i < n_streams; i++)
kernel_1<<<grid, block, 0, streams[i]>>>();
for (int i = 0; i < n_streams; i++)
kernel_2<<<grid, block, 0, streams[i]>>>();
for (int i = 0; i < n_streams; i++)
kernel_3<<<grid, block, 0, streams[i]>>>();
for (int i = 0; i < n_streams; i++)
kernel_4<<<grid, block, 0, streams[i]>>>();
```

Issue order from host: depth-first

![](bbox=[0.095, 0.643, 0.805, 0.668])

FIGURE 6-7

Only the three stream edges are independent.

Using breadth-first ordering ensures that adjacent tasks in the work queue are from different streams (shown in Figure 6-8). Therefore, there is no false dependency between any adjacent pairs of tasks and concurrent kernel execution is possible.

Issue order from host: breadth-first

![](bbox=[0.095, 0.845, 0.805, 0.87])

There is no dependence between any adjacent kernels.

FIGURE 6-8