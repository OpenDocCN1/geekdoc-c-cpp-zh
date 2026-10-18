```
QDP uses OpenMP threading. We have 236 threads
Lattice initialized
  problem size = 32 32 32 64
  layout size = 32 32 32 64
  logical machine size = 1 1 1 1
  subgrid size = 32 32 32 64
  total number of nodes = 1
  total volume = 2097152
  subgrid volume = 2097152
Finished init of RNG
Finished lattice layout
Running Test: timeDslash

              Timing with 50 counts
              50 iterations in 1.988364 seconds
              39767.28 u sec/iteration
              Performance is: 34805.5064364473 Mflops (sp) in Total
              Performance is: 34805.5064364473 per MPI Process

              Timing with 50 counts
              50 iterations in 2.748181 seconds
              54963.62 u sec/iteration
              Performance is: 25182.4810665673 Mflops (dp) in Total
              Performance is: 25182.4810665673 per MPI Process

          OK
Summary: 1 Tests Tried
         1 Tests Succeeded
         0 Tests Failed on some nodes
of which 0 Tests Failed in Unexpected Ways on some nodes
```

![](bbox=[0.115, 0.116, 0.869, 0.468])

Timings of the naive Dslash on an Intel Xeon Phi coprocessor 5110P using 59 cores, or 236 threads. We see a single precision performance of 34.8 GFLOPS in single precision and 25.2 GFLOPS in double precision.

with 2 × 8 cores, and hyperthreading enabled, giving us 32 threads. Further, since we know that the memory allocation in this code is not NUMA aware we used the numactl utility to interleave memory allocation between the sockets using the `numactl --interleave=0,1` command to launch the code. Without enabling the SSE optimization code-branches, the result we obtained on the processor was 34.7 GFLOPS in single precision and 19.3 GFLOPS in double. So a single coprocessor performed roughly as fast (slightly faster) than a dual socket Xeon system using the same code.

While this is not an unreasonable first performance ratio between Intel Xeon processor and Intel Xeon Phi coprocessor, the result is nonetheless somewhat disappointing in terms of absolute performance. Our models tell us that the code should be memory bandwidth bound, so one immediate question is how much memory bandwidth are we utilizing? To answer this we profiled the code using VTune, using its bandwidth collection experiments which reported the code sustaining a memory bandwidth of 42.3 GB/s in the single precision Wilson-Dslash on the Intel Xeon Phi coprocessor.

# EVALUATION OF THE NAIVE CODE

At this point we should pause and reflect. VTune reported that our single precision memory bandwidth on Intel Xeon Phi coprocessor was 42.3 GB/s. Taking the most naive arithmetic intensity of 0.86 FLOP/byte (no caching, no compression, no streaming stores), the model predicts a performance of 36.4 GFLOPS as our maximum. We are sustaining 34.8 GFLOPS of this, which is around 96% of the model prediction. However, the 42.3 GB/s is quite a low bandwidth for the Intel Xeon Phi coprocessor.