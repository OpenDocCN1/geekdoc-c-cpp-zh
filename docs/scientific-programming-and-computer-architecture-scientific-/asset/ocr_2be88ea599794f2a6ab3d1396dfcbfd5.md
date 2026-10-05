# 8.2. Introduction to CUDA

The only parameter we vary when launching threads is the total number of blocks, which is denoted NBLK later. This is typically at least equal to BLKinMP*NMP, or 26, but can be much larger.

# Summing with help from the Leibniz CPU

Our first program for summing the Leibniz series

$\pi = \frac{4}{1} - rac{4}{3} + \frac{4}{5} - \dots$$

on the K20 does not in fact sum the series entirely. It leaves part of the work to the AVX host. To begin, we give the skeleton of the function that runs on the graphics device while omitting its body.^4

```
1 __global__ void
2 __launch_bounds__(THInBLK, BLKinMP)
3 leibniz(long int n, double *result){
4
5 }
```

Evidently, the definition of the leibniz function begins in a manner that is quite different from the C++ function definitions we are used to. It looks different because this function runs on the graphics device and not the x86 host.

The __global__ keyword on line 1 is part of the C language extensions in the CUDA framework. The __global__ qualifier indicates that the ensuing function definition is meant to run on the graphics device and do something more. Not all functions that run on the graphics device are equal. Some of them can be called only from functions that run on the graphics device, and some can be called only from functions that run on the host processor. The __global__ introduces a device function that can be called from the host. Such functions are kernels. Device functions that can be called only by kernels or other device functions are introduced using __device__. We encounter such functions later.

Line 2 gives the launch parameters for this kernel. The launch parameters give the number of threads in a thread block and the number of blocks expected to be

> ^4In addition to documentation from NVIDIA, CUDA programming is explained in Sanders and Kandrot (2010) and Kirk and Hwu (2010).