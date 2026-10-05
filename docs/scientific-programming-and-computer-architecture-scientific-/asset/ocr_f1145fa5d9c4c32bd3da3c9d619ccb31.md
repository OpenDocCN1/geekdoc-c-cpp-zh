```
for(int j=0; j < n; j+=B)
for(int ii=0; ii < B; ii++)
for(int jj=0; jj < B; jj++)
 b[j+jj+(ii+jj)*ldb] = a[i+ii+(j+jj)*m];
```

The leading dimension of the $m \times n$ matrix stored in $a[]$$ is assumed to be $m$, while the leading dimension of the transposed $n \times m$ matrix in $b[]$ is $ldb$, which may be $n$ or greater.

When all 16 cores of the 2.7 GHz AVX host work together, bandwidth to memory realized during transpose is 34 GB/s. For 244 threads on 61 cores of the Phi, the bandwidth is 50 GB/s. In either case, the bandwidth is nearly the same for block sizes $B=25, 50, 100$.

+   7.1.1. Explain how using a hardware picker that picks threads between every core of the Phi can help with bandwidth to memory.

+   7.1.2. Estimate the Xeon Phi's bandwidth to memory when transposing a square matrix in place.

# 7.2 Offload

The offload mode$^{10}$ has been a stable way to program the Phi device since the beginning. The "hello" program has shown us that the syntax for writing Phi programs is virtually identical to the syntax for writing ordinary C/C++ programs. In offload mode, the master of the main program is assumed to be on the host. However, the program holds several segments that are meant to be outsourced to the Phi devices.

In section 7.2.1, we write a simple function called `mic_init()`. Most of the time, the only thing that needs to be changed when an OpenMP program is run on a Phi/MIC device is the number of threads. Typically, the Phi has more cores, and the number of threads on the Phi is four times the number of cores. The `mic_init()` function sets the number of threads correctly for the host as well as the Phi/MIC device once and for all.

> $10}$If the Xeon Phi architecture moves away from the coprocessor model, this section will cease to be relevant.