Double-precision values can be configured and tested using:

```
$ nvcc -arch=sm_20 --DOUBLE_PREC -DVALIDATE nbody.cu -o nbody
$ ./nbody
```

Using double-precision floating-point values
Running host simulation. WARNING, this might take a while.
Any points beyond bounds true; # points exceeded velocity 30251/30720
Total execution time 60688
Error = 3.6643952850002815396e00

The 6 times show of overall execution time when using double-precision-floating! That is a high price for increased accuracy, but a necessity in many applications. Recalling from earlier analysis of the floating-point-perf.cu example that this slowdown is caused by a combination of:

+   1. Doubled host cost twice the length of the float primitive
2. Increased I/O costs on the device load twice as much data from global memory
3. Reduced resources to cache each thread in a thread block as fewer fits registers than floats, potentially leading to more spills of variables to global memory
4. Increased computational cost to perform arithmetic operations on twice the number of bits

Note that the compilation also included a -VALIDATE flag. In Nbody, this adds a test for the numerical accuracy of the results by comparing the output from CUDA against the host implementation. The error printed is the mean difference between the particles calculated by the host and the device. Using double-precision-floating point values shows a clear improvement in precision, though there is still a significant difference between the values computed by CUDA and the host with the CUDA compiler.

Finally, it is also important to study how performance changes when standard or intrinsic functions are enabled using the various compiler flags discussed. Recalling from Table 7-3 that --fft, --prec-div, --prec-sqrt, and --fmad can affect performance and accuracy individually, and that --use_fast_math sets all of those options to maximize performance while auto-selecting intrinsic functions in their standard performance. Table 7-8 shows a sample of execution times and numerical errors achieved with each flag set to its most numerically stable or optimized state. These executions were performed with single-precision values.

# TABLE 7-8: Changes to Nbody Performance and Accuracy with Compiler Flags

| DESCRIPTION | --fft | --prec-div | --prec-sqrt | --fmad | --use_fast math | TIME (MS) | ERROR |
|---|---|---|---|---|---|---||
| All flags set to maximize performance | True | False | False | True | True | 5336 | 4.6944 |
| All flags set to maximize numerical accuracy | False | True | False | False | False | 12042 | 0.0000 |