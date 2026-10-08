This program also demonstrates the large numerical differences between single-precision results that can accumulate in iterative applications as imprecise outputs from one iteration are used as the next. Iterative applications are therefore more likely to require the use of double-precision values for numerical accuracy.

It is also important to note that because a double-precision value takes twice the space of a single-precision value, when you store a double in a register (declared locally in the kernel), the total register space of a thread block is reduced more than if a float were used. You must be extremely careful to declare precise values for float values (for example pi = 3.14159f); Any improper declarations that omit the "f" (pi = 3.14159) will be automatically promoted by the nvcc compiler to double-precision.

# Summary

The effects of floating-point operations on operation performance and numerical accuracy are not unique to GPUs; you face the same concerns when working with other architectures. However, CUDA and GPUs have these unique qualities:

+   - Added host-device communication with double-precision values

+   - Added global I/O with double-precision values

+   - Loss of numerical accuracy due to aggressive floating-point optimizations by the CUDA compiler

In general, if accuracy is paramount for your application then double-precision values are a must. Otherwise, single-precision values can help you reap performance benefits. Table 7-2 summarizes the lessons learned using floating-point operations in CUDA.

TABLE 7-2: Performance, Accuracy, and Correctness of Single- and Double-Precision Floating-Point

| PERFORMANCE | ACCURACY | CORRECTNESS |
|---|---|--|
| SINGLE-PRECISION FLOATING-POINT | Better; less communication and slightly improved computational throughput | Good; only uses 32 bits to store values; not only the range of minimum and maximum values smaller but also the granularity which values can be represented as larger. | No change; no protection against multi-threaded unsafe accesses |
| DOUBLE-PRECISION FLOATING-POINT | Good; as a result of twice the bits having to be transferred to the GPU and values being operated on | Better; wider range as well as improved accuracy thanks to 64 bits of storage | No change; no protection against multi-threaded unsafe accesses |