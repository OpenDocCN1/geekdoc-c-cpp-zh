The result is:

```
/a.out Starting..
Using Device 0: Tesla M2070
Matrix size nx 16384 ny 16384
Matrix: initialization
elapsed 0.397689 sec
sumMatrixOnGPUMix << ((512,16384), (32,1)>>> elapsed 0.037327 sec
Arrays match.
```

Now, increase the block size to 256 as follows:

```
dim3 block(256);
```

Then compile and run it, and the system will report the best performance so far (shown in Table 2-4):

```
sumMatrixOnGPUMix << ((64,16384), (256,1)>>> elapsed 0.030765 sec
```

TABLE 2-4: Results Comparison of Different Kernel Implementations

| KERNEL | EXECUTION CONFIGURE | TIME ELAPSED |
|---|---||
| sumMatrixOnGPUMD2 | (512,1024), (32,16) | 0.038041 |
| sumMatrixOnGPUMD1 | (128,128) | 0.044701 |
| sumMatrixOnGPUMix | (64,16384), (256,1) | 0.030765 |

From the matrix addition examples, you can see several things:

+   - Changing execution configurations affects performance.
- A naive kernel implementation does not generally yield the best performance.
- For a given kernel, trying different grid and block dimensions may yield better performance.

In Chapter 3, you will learn more about what causes these issues from a hardware perspective.

# MANAGING DEVICES

NVIDIA provides several means by which you can query and manage GPU devices. It is important to learn how to query this information, you can use it to set the kernel execution configuration at runtime.

You will learn the two basic and powerful means to query and manage GPU devices in this section:

+   - The CUDA API functions
- The NVIDIA Systems Management Interface (nvidia-smi) command-line utility