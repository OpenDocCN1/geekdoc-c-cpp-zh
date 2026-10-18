
with a version of memcpy that is highly Vectorized and optimized for caching. This has a huge role to play considering that memcpy across the PCIe bus results in full cache line transactions.

- Disable power management options on both the Intel Xeon processor host and the Intel Xeon Phi Coprocessor. While power management allows the processor subsystems to go into sleep states, also called C-states, when it is not actively executing instructions (idle), there is an associated latency of both entering and exiting the lower power states from when it is operating normal (called C0) mode. In other words, while deeper sleep states (e.g., C6) result in larger power savings in a system, the latency of exiting such a deep state is higher and is detrimental to applications that are very sensitive to latency—think of what would happen if the threads on the coprocessor went idle for a period of time that was long enough for the processor to enter a deep sleep state and a packet arrived that required the thread to wake up and start running to process the packet. While most operating systems such as Linux enable power management by default, it is advisable to disable power management before running a latency sensitive application. On Linux this is easily done via a kernel command line called intel_idle.max_cstate=0

## RESULTS

Using the optimizations described above, we transformed the sample code provided. We ran the sample code with two different payload sizes—50 bytes and 1500 bytes. Also, different values for “inter packet gap” were chosen—0, 10 and 100 µs”—defined as publishing frequency.

When the payload was ~50 bytes (as shown in Figure 7.14), the mean latencies were within the expected range (~10 µs) but the tails were quite high (~460 µs when publishing frequency was 10 µs). With 1500 byte payloads (as shown in Figure 7.15) even the mean latencies were in the

| Publishing Frequency (µs) | Mean RTT (µs) | 50% | 70% | 90% | 99% | 99.99% | 100% |
|---|---|---|---|---|---|---|---|
| 0 | 3870.08 | 3808 | 4046 | 4083 | 4122 | 4122 | 4387 |
| 10 | 11.15 | 11 | 11 | 12 | 13 | 374 | 460 |
| 100 | 10.83 | 11 | 11 | 12 | 12 | 59 | 309 |

### FIGURE 7.14

Initial implementation (without optimizations) with 50 byte payload.

| Publishing Frequency (µs) | Mean RTT (µs) | 50% | 70% | 90% | 99% | 99.99% | 100% |
|---|---|---|---|---|---|---|---|
| 0 | 113,531 | 114,119 | 114,233 | 114,284 | 114,499 | 115,004 | 115,114 |
| 10 | 113,427 | 114,075 | 114,193 | 114,237 | 114,315 | 114,551 | 114,561 |
| 100 | 88,196 | 106,920 | 106,999 | 106,699 | 107,131 | 107,181 | 107,224 |

### FIGURE 7.15

Initial implementation (without optimizations) with 1500 byte payload.

| Publishing Frequency (μs) | Mean RTT (μs) | 50% | 70% | 90% | 99% | 99.99% | 100% |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 0 | 2538 | 2560 | 2568 | 2580 | — | — | 2588 |
| 10 | 3.85 | 4 | 4 | 4 | 5 | 21 | 46 |
| 100 | 3.84 | 4 | 4 | 4 | 5 | 19 | 34 |

### FIGURE 7.16

Results after optimizing the code with 50 byte payload.

| Publishing Frequency (μs) | Mean RTT (μs) | 50% | 70% | 90% | 99% | 99.99% | 100% |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 0 | 8808 | 8900 | — | — | 8938 | — | 9085 |
| 10 | 16.04 | 16 | 16 | 16 | 37 | 114 | 155 |
| 100 | 15.81 | 16 | 16 | 16 | 18 | 116 | 224 |

### FIGURE 7.17

Results after optimizing the code with 1500 byte payload.

|  | Without Optimizations | With Optimizations |
|---|---:|---:|
| Mean RTT (μs) | 113,427 | 16 |
| 100% (μs) | 114,561 | 114 |

### FIGURE 7.18

Performance comparison for interpacket gap of 10 μs and 1500 byte payload.

millisecond range (11.3 ms) and therefore completely unacceptable as a solution. While not shown here, other payload sizes resulted in similar issues.

By following a systematic approach involving tracing the “life of a packet” and applying the optimizations mentioned in this chapter (as shown in the sample code), the results shown in Figure 7.16 and Figure 7.17 were obtained. The optimizations result in dramatic improvements in performance especially in the 1500 byte payload case as shown in Figure 7.18.

## CONCLUSIONS

The Intel Xeon Phi coprocessor provides a general-purpose programming environment for applications that benefit from having many independent threads of execution, wide vectors for data processing, large amounts of memory bandwidth and a PCIe interface that provides a high bandwidth and low-latency mechanism to share memory between the host and coprocessors in the system. Using the example of a packet processing engine this chapter presented several key optimization techniques that can significantly increase the performance of the application as well as help achieve the low-latency solution desired by the application. The optimizations include:

- 1. Ensure that the right API is being used for the application. Bandwidth sensitive applications benefit from using the DMA engine even though this involves a transition into the kernel. Latency sensitive applications, on the other hand, benefit from APIs that are able to avoid ring transitions and SCIF provides methods to implement such techniques.
- 2. Taking advantage of the fact that coprocessor memory is mapped write combining allows an application to effectively combine larger amounts of data before they are pushed across the PCIe bus resulting in higher protocol efficiency.
- 3. Conversion of PCIe read transactions into write transactions results in significant performance improvements because of the posted nature of the latter.
- 4. Avoiding expensive and unnecessary reads across the PCIe bus in the implementation of a FIFO for full and empty checks by shadowing the head and tail pointers provides additional benefits without any loss in correctness of the code.
- 5. Tickless kernels play a big role in reducing overall jitter and run-to-run variability in applications running on a general-purpose OS such as Linux. Avoiding constant interruptions from the OS, and the associated TLB and cache pollution, translate into additional application performance gains.
- 6. Thread affinity, via standard pthreads APIs or a runtime provided environment variable allow the placement of threads avoiding both oversubscription and load imbalance issues. It also keeps the kernel scheduler from having to load balance threads across the system resulting in lower kernel involvement.
- 7. Finally, use of several simple, yet effective, miscellaneous optimizations, such as the use of a compiler generated vectorized memcpy as well as careful consideration of power management can result in higher performance and lower latency impacts on an application.

## FOR MORE INFORMATION

- Symmetric Communication InterFace (SCIF) User’s guide in MPSS: https://software.intel.com/en-us/articles/intel-manycore-platform-software-stack-mpss.
- A discussion on the Symmetric Communication InterFace (SCIF) APIs—https://software.intel.com/de-de/forums/topic/393771.
- Section 11.3, Intel® 64 and IA-32 Architectures Software Developer’s Manual, Combined volumes 1, 2A, 2B, 2C, 3A, 3B and 3C, January 2015.
- Write Combining Memory Implementation Guidelines http://download.intel.com/design/pentiumii/applnots/24442201.pdf.
- Previewing tickless support for Linux on the Intel® Xeon Phi Coprocessor: https://software.intel.com/en-us/articles/previewing-tickless-support-for-linux-on-the-intel-xeon-phi-coprocessor.
- Processor power management: https://people.cs.pitt.edu/~kirk/cs3150spring2010/ShiminChen.pptx.
- Download the code from this, and other chapters, http://lotsofcores.com.

This page intentionally left blank

## PARALLEL NUMERICAL METHODS IN FINANCE

Shuo Li
Intel Corporation, USA

## OVERVIEW

In the realm of scientific calculations, many problems are expressed using nonlinear equations. The same is true for quantitative finance problems such as computing implied volatility or computing the yield of fixed coupon bonds. There are several well-known numerical methods for solving nonlinear equations. The simplest of all is the bisection method and the most popular is Newton-Raphson method.

In this chapter, we utilize a slightly more complicated example, American option pricing, and develop a C/C++ program that use the Newton-Raphson method to find solutions to partial differential equations based on the Black-Scholes model. We demonstrate how the principles of high performance parallel computing can be applied to the numerical approximation in general and Newton-Raphson in Finance specifically.

The first part of this chapter focuses on the quantitative finance and numerical methods of this problem. We start by reviewing the challenges in pricing American options. Next, we derive the pricing equation for American options using approximation techniques. In the final section, we develop a C/C++ implementation of the Newton-Raphson method.

The second part of this chapter applies a systematic approach to the program we developed in the first part. We start by fine-tuning the numerical operations in the initial program to arrive at a scalar-optimized implementation. Next, we introduce SIMD parallelism. The vector-optimized version of the program is then derived. Next, we introduce thread and core parallelism. We will see how OpenMP 4.0 can be applied to the program to create scalar parallel and vector parallel programs.

Finally, we compare the performance of various versions of the program and demonstrate the benefit of several high-performance techniques and postulate how the same methodology can be applied to other types of numerical approximation to achieve superior performance results.

## INTRODUCTION

In the prior Pearls book, Chapter 19, covered the Black-Scholes model and the Black-Scholes formula to price European options. Thereby, applying high-performance computing methods to achieve high performance on the European style option pricing algorithm. However, nearly all the options written on a wide variety of underlying financial products including stocks, commodities and foreign exchanges are the American style with an early exercise clause included into the contracts. Unlike the European style option pricing problems, there is no close-form solution for the American style option pricing
