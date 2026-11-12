```
CUTThread thread = start_thread( routine, &(data[1]) );
routine( &(data[0]) );
end_thread( thread );
```

Because our host memory was allocated by the CUDA runtime, we use cudaFreeHost() to free it. Other than no longer calling free(), we have seen all there is to see in main().

```
// free memory on the CPU side
HANDLE_ERROR( cudaFreeHost( a ) );
HANDLE_ERROR( cudaFreeHost( b ) );

printf( "Value calculated: %f\n",
        data[0].returnValue + data[1].returnValue );

return 0;
}
```

To support portable pinned memory and zero-copy memory in our multi-GPU application, we need to make two notable changes in the code for routine(). The first is a bit subtle, and in no way should this have been obvious.

```
void* routine( void* pvoidData ) {
    DataStruct *data = (DataStruct*)pvoidData;

    if (data->deviceID != 0) {
        HANDLE_ERROR( cudaSetDevice( data->deviceID ) );
        HANDLE_ERROR( cudaSetDeviceFlags( cudaDeviceMapHost ) );
    }
}
```

You recall in our multi-GPU version of this code, we need a call to cudaSetDevice() in routine() in order to ensure that each participating thread controls a different GPU. On the other hand, in this example we have already made a call to cudaSetDevice() from the main thread. We did so in order to allocate pinned memory in main(). As a result, we only want to call