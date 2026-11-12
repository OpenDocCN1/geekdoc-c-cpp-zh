```
// Wait for stop event
CUDA_CALL(cudaEventSynchronize(kernel_stop));

// Get delta between start and stop,
// i.e. the kernel execution time
float delta = 0.0f;
CUDA_CALL(cudaEventElapsedTime(&delta, kernel_start, kernel_stop));

// Clean up
CUDA_CALL(cudaFree(device_src_ptr));
CUDA_CALL(cudaFree(device_dest_ptr));
CUDA_CALL(cudaEventDestroy(kernel_start));
CUDA_CALL(cudaEventDestroy(kernel_stop));
CUDA_CALL(cudaStreamDestroy(test_stream));

return delta;
}
```

When we run this code, we achive the following results:

+   Running Interleaved / Non Interleaved memory test using 65536 bytes (4096 elements)
+   ID:0 GeForce GTX 470: Interleaved time: 181.83ms
+   ID:0 GeForce GTX 470: Non Interleaved time: 45.13ms
+   ID:1 GeForce 9800 GT: Interleaved time: 2689.15ms
+   ID:1 GeForce 9800 GT: Non Interleaved time: 234.98ms
+   ID:2 GeForce GTX 260: Interleaved time: 444.16ms
+   ID:2 GeForce GTX 260: Non Interleaved time: 139.35ms
+   ID:3 GeForce GTX 460: Interleaved time: 199.15ms
+   ID:3 GeForce GTX 460: Non Interleaved time: 63.49ms
+   CPU (serial): Interleaved time: 1216.00ms
+   CPU (serial): Non Interleaved time: 13640.00ms

What we see is quite interesting, and largely to be expected. The interleaved memory access pattern has an execution time three to four times longer than the noninterleaved pattern on compute 2.x hardware. The compute 1.3 GTX260 demonstrates a 3x slow down when using the interleaved memory pattern. The compute 1.1 9800GT, however, exhibits a 11x slow down, due to the more stringent coalescing requirements for these older devices.

We can look a bit deeper into the memory access pattern between the slow interleaved pattern and the much faster noninterleaved pattern with a tool such as Parallel Nsight. We can see that the number of memory transactions (CUDA Memory Statistics experiment) used in the noninterleaved version is approximately one-quarter that of the interleaved version, resulting in the noninterleaved version shifting one-quarter of the data to/from memory than the interleaved version does.

One other interesting thing to note is the CPU shows exactly the opposite effect. This may seem strange, until you think about the access pattern and the cache reuse. A CPU accessing element a in the