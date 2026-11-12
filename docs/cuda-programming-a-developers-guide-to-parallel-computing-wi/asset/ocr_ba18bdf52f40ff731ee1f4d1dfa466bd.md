We also need to redefine the kernel so it does considerably more work, so we can actually see some reasonable execution times on the kernel:

```
__global__ void gpu_test_kernel(u32 * data, const u32 iter)
{
    const int tid = (blockIdx.x * blockDim.x)
            + threadIdx.x;

    for (u32 i=0; i<iter; i++)
    {
        data[tid] *= 2;
        data[tid] /= 2;
    }
}
```

When we run the program we see the following result:

```
ID:0 GeForce GTX 470:Copy To         :  20.22 ms
ID:0 GeForce GTX 470:Kernel          : 4883.55 ms
ID:0 GeForce GTX 470:Copy Back       :  10.11 ms
ID:0 GeForce GTX 470:Component Time  : 4913.78 ms
ID:0 GeForce GTX 470:Execution Time  : 4913.78 ms
ID:0 GeForce GTX 470:Array check passed

ID:1 GeForce 9800 GT:Copy To         :  20.77 ms
ID:1 GeForce 9800 GT:Kernel          : 25279.57 ms
ID:1 GeForce 9800 GT:Copy Back       :  10.02 ms
ID:1 GeForce 9800 GT:Component Time  : 25310.37 ms
ID:1 GeForce 9800 GT:Execution Time  : 25310.37 ms
ID:1 GeForce 9800 GT:Array check passed

ID:2 GeForce GTX 260:Copy To         :  20.88 ms
ID:2 GeForce GTX 260:Kernel          : 14268.92 ms
ID:2 GeForce GTX 260:Copy Back       :  10.00 ms
ID:2 GeForce GTX 260:Component Time  : 14299.80 ms
ID:2 GeForce GTX 260:Execution Time  : 14299.80 ms
ID:2 GeForce GTX 260:Array check passed

ID:3 GeForce GTX 460:Copy To         :  20.11 ms
ID:3 GeForce GTX 460:Kernel          : 6652.78 ms
ID:3 GeForce GTX 460:Copy Back       :   9.94 ms
ID:3 GeForce GTX 460:Component Time  : 6682.83 ms
ID:3 GeForce GTX 460:Execution Time  : 6682.83 ms
ID:3 GeForce GTX 460:Array check passed
```

You can see from the results that the memory copy operations are within a small tolerance of one another. This is not too surprising as each device is running on an x8 PCI-E 2.0 link. The PCI link speed is considerably slower than even the slowest device's memory speed, so we are in fact limited by the PCI-E bus speed with regard to such transfers.