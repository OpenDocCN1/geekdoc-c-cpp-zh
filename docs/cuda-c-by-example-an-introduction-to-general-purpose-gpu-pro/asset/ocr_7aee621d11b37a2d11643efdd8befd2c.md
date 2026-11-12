```
// enqueue copies of c from device to locked memory
HANDLE_ERROR( cudaMemcpyAsync( host_c_i, dev_c0,
    N * sizeof(int),
    cudaMemcpyDeviceToHost,
    stream0 ) );
HANDLE_ERROR( cudaMemcpyAsync( host_c_i+N, dev_c1,
    N * sizeof(int),
    cudaMemcpyDeviceToHost,
    stream1 ) );
}
```

If we assume that our memory copies and kernel executions are roughly comparable in execution time, our new execution timeline will look like Figure 10.5. The interengine dependencies are highlighted with arrows similar to illustrate that they are still satisfied with this new scheduling order.

Because we have queued our operations breadth-first across streams, we no longer have stream 0's copy of c blocking stream 1's initial memory copies of a and b. This allows the GPU to execute copies and kernels in parallel, allowing our application to run significantly faster. The new code runs in 48ms, a 21 percent improvement over our original, naive double-stream implementation. For applications that can overlap nearly all computation and memory copies, you can approach a nearly twofold improvement in performance because the copy and kernel engines will be cranking the entire time.

![](bbox=[0.19, 0.63, 0.68, 0.89])