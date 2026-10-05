# 7.3. Two examples: FFT and matrix multiplication

| n | AVX (host) | MIC (native) | MIC (offload) | MKL Auto |
| 8,000 | 352 GF/s | 837 GF/s | 299 GF/s | 731 GF/s |
| 10,000 | 333 GF/s | 845 GF/s | 365 GF/s | 926 GF/s |
| 12,000 | 339 GF/s | 859 GF/s | 412 GF/s | 1214 GF/s |

Table 7.5: Floating point bandwidths in GFLOps/sec.

the floating point throughput is slightly greater than the theoretical limit of 345.6 GFLOps/s. The discrepancy is probably because the in-core “turbo” frequency of 3.5 GHz is near the input clock frequency of 2.7 GHz.

The MIC device reaches nearly 85% of its peak floating point throughput when run natively. Offloading the function `result()` to MKL does not do so well for unknown reasons. MKL appears to be set up for automatic offload. If part of the computation is to be offloaded to a device, it is better to leave the offloading to MKL. With automatic offloading and $n = 12,000$, MKL manages to nearly sum the floating point throughputs of the MIC device and the AVX host to reach 1.2 TFLOps/sec.$^{14}$

**Exercise 7.3.1.** The name of the function `asm8x1x8()` is mangled according to C++ conventions. Unmangle the name and supply a header file to make the function callable from both C and C++.

**Exercise 7.3.2.** Write an LU factorization routine for the AVX-512 instruction set of the Xeon Phi. Compare with the speed of MKL library’s implementation of the same function. By what factor do you expect your routine to fall short if it does not use any instruction-level optimizations?

> $^{14}$The 1 TFLOps/sec barrier was crossed by a supercomputer for the first time in 1997.