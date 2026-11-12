```
// Wait for everything to complete
for (ui32 i=0; i < NUM_STREAMS; i++)
{
    CUDA_CALL(cudaStreamSynchronize(async_stream[i]));
}

// Grab the end time
TIMER_T delta_time_device_async = get_time() - start_time_device;

// Compare the device data with the host calculated version
for (ui32 i=0; i < NUM_STREAMS; i++)
{
    compare_results(host_dst_ptr[i], host_dst_ptr2, num_bytes, "\nMulti Stream
Comparison between CPU and GPU processing:");
}

printf("\nCPU Time: %.1f, GPU Sync Time: %.1f, GPU Async Time: %.1f", delta_time_cpu,
delta_time_device, delta_time_device_async);

// Free host and device memory
for (ui32 i=0; i < NUM_STREAMS; i++)
{
    CUDA_CALL(cudaFree(device_src_ptr[i]));
    CUDA_CALL(cudaFree(device_src_ptr2[i]));
    CUDA_CALL(cudaFree(device_dst_ptr[i]));
    CUDA_CALL(cudaFree(device_dst_ptr2[i]));
    CUDA_CALL(cudaFreeHost(host_src_ptr[i]));
    CUDA_CALL(cudaStreamDestroy(async_stream[i]));
}

CUDA_CALL(cudaFreeHost(host_src_ptr1));
CUDA_CALL(cudaFreeHost(host_src_ptr2));
CUDA_CALL(cudaFreeHost(host_dst_ptr2));

// Reset the device so it's clear for next time
CUDA_CALL(cudaDeviceReset());
}
```

The major difference we see with the streamed version is that we now need multiple output data blocks on the host as well as multiple copies on the device. Thus, all the device arrays are now indexed by [NUM_STREAMS], allowing the streams to operate entirely separately and independently of one another. To use the asynchronous model we need to allocate host memory as pinned, so we have to use cudaHostMalloc instead of malloc, paired with cudaFreeHost instead of free. We also need to wait on the completion of the stream prior to processing its data. In this example we wait on all four streams, but in reality as one stream completes, it would be provided with more work. See Chapters 8 and 9 regarding multi-GPU programming and optimization, respectively, to see how this works.