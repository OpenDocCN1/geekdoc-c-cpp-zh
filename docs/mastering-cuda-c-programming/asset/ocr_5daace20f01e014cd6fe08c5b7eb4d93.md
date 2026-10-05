# Launching Kernels

Kernels are called using a specific syntax that indicates the execution configuration, which includes the number of threads and thread blocks. The syntax for launching a kernel is as follows:

```
blockSize>>>(parameters);
```

the number of blocks that will be used for the kernel's execution.
the number of threads in each block.

This syntax is unique to CUDA and is essential for specifying how the parallel computation should be distributed across the GPU's architecture.