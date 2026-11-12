
| Limit | Behavior |
|---|---|
| | and the thread's last error will be set to cudaErrorLaunchPendingCountExceeded. The default pending launch count is 2048 launches. |
| cudaLimitStackSize | Controls the stack size in bytes of each GPU thread. The CUDA driver automatically increases the per-thread stack size for each kernel launch as needed. This size isn't reset back to the original value after each launch. To set the per-thread stack size to a different value, cudaDeviceSetLimit() can be called to set this limit. The stack will be immediately resized, and if necessary, the device will block until all preceding requested tasks are complete. cudaDeviceGetLimit() can be called to get the current per-thread stack size. |

### D.4.3.1.5. Memory Allocation and Lifetime

cudaMalloc() and cudaFree() have distinct semantics in different environments. When invoked from the host, cudaMalloc() allocates a new region from unused device memory. When invoked from the device runtime these functions map to device-side malloc() and free(). This implies that within the device environment the total allocatable memory is limited to the device malloc() heap size, which may be smaller than the available unused device memory. Also, it is an error to invoke cudaFree() from the host program on a pointer which was allocated by cudaMalloc() on the device or vice-versa.

| | cudaMalloc() on Host | cudaMalloc() on Device |
|---|---|---|
| cudaFree() on Host | Supported | Not Supported |
| cudaFree() on Device | Not Supported | Supported |
| Allocation limit | Free device memory | cudaLimitMallocHeapSize |

### D.4.3.1.6. SM Id and Warp Id

Note that in PTX %smid and %warpid are defined as volatile values. The device runtime may reschedule thread blocks onto different SMs in order to more efficiently manage resources. As such, it is unsafe to rely upon %smid or %warpid remaining unchanged across the lifetime of a thread or thread block.

### D.4.3.1.7. ECC Errors

No notification of ECC errors is available to code within a CUDA kernel. ECC errors are reported at the host side once the entire launch tree has completed. Any ECC errors which arise during execution of a nested program will either generate an exception or continue execution (depending upon error and configuration).

## Appendix E.
MATHEMATICAL FUNCTIONS

The reference manual lists, along with their description, all the functions of the C/C++ standard library mathematical functions that are supported in device code, as well as all intrinsic functions (that are only supported in device code).

This appendix provides accuracy information for some of these functions when applicable.

### E.1. Standard Functions

The functions from this section can be used in both host and device code.

This section specifies the error bounds of each function when executed on the device and also when executed on the host in the case where the host does not supply the function.

The error bounds are generated from extensive but not exhaustive tests, so they are not guaranteed bounds.

### Single-Precision Floating-Point Functions

Addition and multiplication are IEEE-compliant, so have a maximum error of 0.5 ulp.

The recommended way to round a single-precision floating-point operand to an integer, with the result being a single-precision floating-point number is `rintf()`, not `roundf()`. The reason is that `roundf()` maps to a 4-instruction sequence on the device, whereas `rintf()` maps to a single instruction. `truncf()`, `ceilf()`, and `floorf()` each map to a single instruction as well.

### Table 7 Single-Precision Mathematical Standard Library Functions with Maximum ULP Error

The maximum error is stated as the absolute value of the difference in ulps between a correctly rounded single-precision result and the result returned by the CUDA library function.

| Function | Maximum ulp error |
| :--- | :--- |
| x+y | 0 (IEEE-754 round-to-nearest-even) |
| x*y | 0 (IEEE-754 round-to-nearest-even) |
| x/y | 0 for compute capability ≥ 2 when compiled with -prec-div=true<br>2 (full range), otherwise |
| 1/x | 0 for compute capability ≥ 2 when compiled with -prec-div=true<br>1 (full range), otherwise |
| rsqrtf(x) | 2 (full range) |
| 1/sqrtf(x) | Applies to 1/sqrtf(x) only when it is converted to rsqrtf(x) by the compiler. |
| sqrtf(x) | 0 when compiled with -prec-sqrt=true<br>Otherwise 1 for compute capability ≥ 5.2<br>and 3 for older architectures |
| cbrtf(x) | 1 (full range) |
| rcbrtf(x) | 1 (full range) |
| hypotf(x, y) | 3 (full range) |
| rhypotf(x, y) | 2 (full range) |
| norm3df(x, y, z) | 3 (full range) |
| norm3df(x, y, z) | 2 (full range) |
| norm4df(x, y, z, t) | 3 (full range) |
| rnorm4df(x, y, z, t) | 2 (full range) |
| normf(dim, arr) | An error bound can't be provided because a fast algorithm is used with accuracy loss due to round-off |
| rnormf(dim, arr) | 3 (full range) |
| expf(x) | 2 (full range) |
| exp2f(x) | 2 (full range) |
| exp10f(x) | 2 (full range) |
| expm1f(x) | 1 (full range) |
| logf(x) | 1 (full range) |
| log2f(x) | 1 (full range) |
| log10f(x) | 2 (full range) |
| log1pf(x) | 1 (full range) |
| sinf(x) | 2 (full range) |
| cosf(x) | 2 (full range) |
| tanf(x) | 4 (full range) |
| sincosf(x, sptr, cptr) | 2 (full range) |
| sinpif(x) | 2 (full range) |
| cospif(x) | 2 (full range) |
| sincospif(x, sptr, cptr) | 2 (full range) |
| asinf(x) | 4 (full range) |
| acosf(x) | 3 (full range) |
| atanf(x) | 2 (full range) |
| atan2f(y, x) | 3 (full range) |
| sinhf(x) | 3 (full range) |
| coshf(x) | 2 (full range) |
| tanhf(x) | 2 (full range) |
| asinhf(x) | 3 (full range) |
| acoshf(x) | 4 (full range) |
| atanhf(x) | 3 (full range) |
| powf(x, y) | 8 (full range) |
| erff(x) | 2 (full range) |
| erfcf(x) | 4 (full range) |
| erfinvf(x) | 2 (full range) |
| erfcinvf(x) | 2 (full range) |
| erfcxf(x) | 4 (full range) |
| normcdff(x) | 5 (full range) |
| normcdfinvf(x) | 5 (full range) |
| lgammaf(x) | 6 (outside interval -10.001 ... -2.264; larger inside) |
| tgammaf(x) | 11 (full range) |
| fmaf(x, y, z) | 0 (full range) |
| frexpf(x, exp) | 0 (full range) |
| ldexpf(x, exp) | 0 (full range) |
| scalbnf(x, n) | 0 (full range) |
| scalblnf(x, l) | 0 (full range) |
| logbf(x) | 0 (full range) |
| ilogbf(x) | 0 (full range) |
| j0f(x) | 9 for \|x\| < 8 otherwise, the maximum absolute error is 2.2 x 10^6 |
| j1f(x) | 9 for \|x\| < 8 otherwise, the maximum absolute error is 2.2 x 10^6 |
| jnf(x) | For n = 128, the maximum absolute error is 2.2 x 10^6 |
| y0f(x) | 9 for \|x\| < 8 otherwise, the maximum absolute error is 2.2 x 10^6 |
| y1f(x) | 9 for \|x\| < 8 otherwise, the maximum absolute error is 2.2 x 10^6 |
| ynf(x) | ceil(2 + 2.5n) for \|x\| < n otherwise, the maximum absolute error is 2.2 x 10^6 |
| cyl_bessel_i0f(x) | 6 (full range) |
| cyl_bessel_i1f(x) | 6 (full range) |
| fmodf(x, y) | 0 (full range) |
| remainderf(x, y) | 0 (full range) |
| remquof(x, y, iptr) | 0 (full range) |
| modff(x, iptr) | 0 (full range) |
| fdimf(x, y) | 0 (full range) |
| truncf(x) | 0 (full range) |
| roundf(x) | 0 (full range) |
| rintf(x) | 0 (full range) |
| nearbyintf(x) | 0 (full range) |
| ceilf(x) | 0 (full range) |
| floorf(x) | 0 (full range) |
| lrintf(x) | 0 (full range) |
| lroundf(x) | 0 (full range) |
| llrintf(x) | 0 (full range) |
| llroundf(x) | 0 (full range) |

### Double-Precision Floating-Point Functions

The recommended way to round a double-precision floating-point operand to an integer, with the result being a double-precision floating-point number is rint(), not round(). The reason is that round() maps to a 4-instruction sequence on the device, whereas rint() maps to a single instruction. trunc(), ceil(), and floor() each map to a single instruction as well.

### Table 8 Double-Precision Mathematical Standard Library Functions with Maximum ULP Error

The maximum error is stated as the absolute value of the difference in ulps between a correctly rounded double-precision result and the result returned by the CUDA library function.

| Function | Maximum ulp error |
|---|---|
| x+y | 0 (IEEE-754 round-to-nearest-even) |
| x*y | 0 (IEEE-754 round-to-nearest-even) |
| x/y | 0 (IEEE-754 round-to-nearest-even) |
| 1/x | 0 (IEEE-754 round-to-nearest-even) |
| sqrt(x) | 0 (IEEE-754 round-to-nearest-even) |
| rsqrt(x) | 1 (full range) |
| cbrt(x) | 1 (full range) |
