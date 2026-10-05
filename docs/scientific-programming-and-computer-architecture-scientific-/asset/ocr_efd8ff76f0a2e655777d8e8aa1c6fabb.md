# Chapter 8. Special Topic: Graphics Coprocessor Programming Using CUDA

zero on line 2, merits discussion. The host can talk to the graphics device over several streams, and the second argument can be used to indicate the stream on which the event is recorded. But if the second argument is 0, the event is recorded after all preceding operations in the CUDA context have been completed.

The stop event is recorded by the member function tic() on line 6. When CUDA events are recorded using function calls, such as the ones on lines 2 and 6, the function returns immediately after sending the event to the graphics device. It does not wait until the event is actually recorded. The function calls are nonblocking. The events stop and start are not available to be read on the host immediately after cudaEventRecord(). The calls to cudaEventSynchronize() (lines 7 and 8) block until the events are ready to be read. On line 9, the two events are read, and the time elapsed is calculated.

# 8.1.4 Warps and thread blocks

The K20's design is so different from that of conventional processors to program we need to understand a few things about its architecture. A sketch of its microarchitecture is shown in figure 8.2.

To get a better sense of the microarchitecture, we return to the cudaDeviceProp program of section 7.1 and show some of its output.

```
Total L2 cache (in bytes): 1310720
Shared memory per MP (in bytes): 49152
Number of registers per MP: 65536
Max number of threads per MP: 2048
```

The heart of the microarchitecture is the streaming multiprocessor, and there are 13 of these in Kepler. The K20 has 1.3 MB of L2 cache on chip, a small figure compared to the 20 MB cache of its 2.7 GHz AVX host. The L2 cache is shared by the 13 multiprocessors.

Each multiprocessor has 64 KB of on-chip memory for itself. This memory is split between L1 cache and shared memory. The use of shared memory is under control. On the K20, 48 KB is assigned to shared memory by default, and only 16 KB is left for the L1 cache. The split between L1 cache and shared memory can be changed by calling a function in the CUDA runtime library.