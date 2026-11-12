# CHAPTER 6 Memory Handling with CUDA

```
const_test_gpu_const <<<(num_blocks, num_threads)>>(data_gpu, num_elements);
cuda_error_check("Error ", " returned from constant runtime kernel");
CUDA_CALL(cudaEventRecord(kernel_stop2,0));
CUDA_CALL(cudaEventSynchronize(kernel_stop2));
CUDA_CALL(cudaEventElapsedTime(&delta_time2, kernel_start2, kernel_stop2));
//printf("Inconst Elapsed time : %3.fms", delta_time2);
if (delta_time1 > delta_time2)
printf("****nSConstant version is faster by: %2.fms (G=%2.fms, C=%2.fms)",
device_prefix, delta_time1-delta_time2, delta_time1, delta_time2);
else
printf("****n%sGEM version is faster by: %2.fms (G=%2.fms, C=%2.fms)",
device_prefix, delta_time2-delta_time1, delta_time1, delta_time2);
]
CUDA_CALL(cudaEventDestroy(kernel_start1));
CUDA_CALL(cudaEventDestroy(kernel_start2));
CUDA_CALL(cudaEventDestroy(kernel_stop1));
CUDA_CALL(cudaEventDestroy(kernel_stop2));
CUDA_CALL(cudaFree(data_gpu));
CUDA_CALL(cudaDeviceReset());
printf("n");
}
wait_exit();
}
```

Notice how the cudaMemcpyToSymbol call works. You can copy to any named global symbol on the GPU, regardless of whether that symbol is in global memory or constant memory. Thus, if you chunk the data to 64 K chunks, you can access it from the constant cache. This is very useful if all threads are accessing the same data element, as you get the broadcast and cache effect from the constant memory section.

Notice also that the memory allocation, creation of events, destruction of the events and freeing of device memory is now done outside the main loop. CUDA API calls such as these are actually very costly in terms of CPU time. The CPU load of this program drops considerably with this simple change. Always try to set up everything at the start and destroy or free it at the end. Never do this in the loop body or it will greatly slow down the application.

# Constant question

+   1. If you have a data structure that is 16 K in size and exhibits a random pattern of access per block but a unified access pattern per warp, would it be best to place it into registers, constant memory, or shared memory? Why?