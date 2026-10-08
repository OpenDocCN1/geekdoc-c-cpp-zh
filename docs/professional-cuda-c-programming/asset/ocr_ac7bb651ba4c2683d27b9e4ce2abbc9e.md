You may wonder why the kernel performance nearly doubled just by altering the execution configuration. Intuitively, you may reason that the second configuration has twice as many blocks as the first configuration, so there is twice as much parallelism. The intuition is right. However, if you further reduce the block size to 16 x 16, you quadrupled the number of blocks compared to the first configuration. The result of this configuration, as shown below, is better than the first but worse than the second.

```
sumMatrixOnGPU2D <<< (1024,1024), (16,16) >>> elapsed 0.045535 sec
```

Table 2-3 summarizes the performance for different execution configurations. From the results, you can see that increasing the number of blocks does not necessarily always increase the performance of the kernel. In Chapter 3, you will learn why different execution configurations impact kernel performance.

# TABLE 2-3: Matrix Summation with Different Execution Configuration

| KERNEL CONFIGURATION | KERNEL ELAPSED TIME | BLOCK NUMBER |
| --- | --- | --- |
| (32,32) | 0.060323 sec | 512 x 512 |
| (32,16) | 0.038041 sec | 512 x 1024 |
| (16,16) | 0.045535 sec | 1024 x 1024 |

# Summing Matrices with a 1D Grid and 1D Blocks

To use a 1D grid with 1D blocks, you need to write a new kernel in which each thread processes data elements, as shown in Figure 2-13.

![](bbox=[0.147, 0.613, 0.649, 0.873])

FIGURE 2-13