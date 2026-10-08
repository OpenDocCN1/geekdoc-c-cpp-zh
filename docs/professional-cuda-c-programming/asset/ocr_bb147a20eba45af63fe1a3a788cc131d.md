# 4. Put the following at the end of the main loop in `simpleMultiGPU`:

```
cudaStreamSynchronize(stream[i]);
```

Recompile the code and run it with `nvvp` for both cases of one GPU and two GPU, compare the results with Exercise 9.3 and explain the reason for the difference.

# 5. In `simpleMultiGPU.cu`, move data initialization (`initialData`) to the main kernel loop. Run with `nvvp` to see what changes.

# 6. Refer to the file `simpleP2P_PingPong.cu`. Modify the code section labeled `unidirectional gcpy` to use asynchronous copies.

# 7. Refer to the file `simpleP2P_PingPong.cu`. Add code that ping-pongs between two GPUs based on the bidirectional, asynchronous ping-pong example. Use the function:

```
cudaMemcpyPeerAsync(void* dst, int dstDev, const void* src, size_t count, cudaStream_t stream)
```

# 8. Refer to the file `simpleP2P_PingPong.cu`. Use a default stream in the asynchronous memory copy runtime. Compare the result with a non-default stream.

# 9. Refer to the file `simpleP2P_PingPong.cu`. Disable P2P access first, and then compare results of unidirectional bidirectional memory copy, and synchronous versus asynchronous functions.

# 10. Refer to the file `simpleP2DF.cu`. Rearrange wave propagation with the following logic: (1) calculate halo on stream, (2) exchange halo on stream, (3) calculate on stream internal, and (4) synchronize each device. Compare the results with the original and explain the reason for performance changes.

# 11. Explain how CPU and GPU affinity affect execution time of an application. Suppose you run a CUDA-MPI application with:

```
$ mpirun_hrnp -np 2 node01 MV2_ENABLE_AFFINITY=1 ./simple2c
$ mpirun_hrnp -np 2 node01 MV2_ENABLE_AFFINITY=0 ./simple2c
```

The first command enables GPU affinity, while the second different techniques you would use to establish GPU affinity for each MPI process in the scenarios above, and explain why.

# 12. What is GPUDirect RDMA? How can it improve performance? What are the hardware and software requirements for GPUDirect RDMA?

# 13. How could you use MPI functions, `cudaMemcpyAsync`, and stream callbacks to build an asynchronous version of `simpleP2P.c?