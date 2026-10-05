568 Chapter 8. Special Topic: Graphics Coprocessor Programming Using CUDA

| AVX | Phi | K20 |
| Read b/w | 91 GB/s | 161 GB/s | 137 GB/s |
| Copy b/w | 50 GB/s | 86 GB/s | 133 GB/s |

Table 8.2: Read and copy bandwidths in GB/s. The K20 is compared to the Phi and its 2.7 GHz AVX host (for the full name of the machine, see A.1).

# 8.3.2 Matrix multiplication

If $A, B,$ and $C$ are $N \times N$ matrices, then $C = C + AB$ requires $2N^3$ floating point operations (flops). Half the operations are additions and half are multiplications. The amount of memory used in multiplication is $\mathcal{O}(N^2)$, but the number of flops is $\mathcal{O}(N^3)$. If $N$ is large, there is a possibility that the cost of memory accesses can be hidden almost completely, and the program's speed is determined by the peak floating point bandwidth. On the K20, the peak floating point bandwidth is 1.17 Tflops/s. Although the programs do not approach that speed, we compare them against a cuBLAS program that does.

# Global memory

The first program for multiplying square matrices is follows:^9

```
__global___
__launch_bounds__(THInBLK, BLKInMP)
void mmult_gem(double *A, double *B, double *C,
    int N) {
    int tidx = threadIdx.x;
    int tidy = threadIdx.y;
    int bidx = blockIdx.x;
    int bidity = blockIdx.y;
    int i = bidx*blockDim.x + tidx;
    int j = bidity*blockDim.y + tidy;
    for(int k = 0; k < N; k++)
        C[i+k*N] += A[i+k*N]*B[k*N];
```

> ^9This program is adapted from (CUDA C Programming Guide, August, 2014).