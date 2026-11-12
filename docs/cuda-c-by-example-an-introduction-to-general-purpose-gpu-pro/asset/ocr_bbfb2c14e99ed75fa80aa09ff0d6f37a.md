```
if (lprop.deviceOverlap) {
    printf( "Device will not handle overlaps, so no "
            "speed up from streams\n" );
    return 0;
}

cudaEvent_t     start, stop;
float           elapsedTime;

// start the timers
HANDLE_ERROR( cudaEventCreate( &start ) );
HANDLE_ERROR( cudaEventCreate( &stop ) );
HANDLE_ERROR( cudaEventRecord( start, 0 ) );
```

Next, we create our two streams exactly as we created the single stream in the previous section's version of the code.

```
// initialize the streams
cudaStream_t  stream0, stream1;
HANDLE_ERROR( cudaStreamCreate( &stream0 ) );
HANDLE_ERROR( cudaStreamCreate( &stream1 ) );
```

We will assume that we still have two input buffers and a single output buffer on the host. The input buffers are filled with random data exactly as they were in the single-stream version of this application. However, now that we intend to use two streams to process the data, we allocate two identical sets of GPU buffers so that each stream can independently work on chunks of the input.

```
int *host_a, *host_b, *host_c;
int *dev_a0, *dev_b0, *dev_c0; // GPU buffers for stream0
int *dev_a1, *dev_b1, *dev_c1; // GPU buffers for stream1

// allocate the memory on the GPU
HANDLE_ERROR( cudaMalloc( (void**)&dev_a0,
                          N * sizeof(int) ) );
```