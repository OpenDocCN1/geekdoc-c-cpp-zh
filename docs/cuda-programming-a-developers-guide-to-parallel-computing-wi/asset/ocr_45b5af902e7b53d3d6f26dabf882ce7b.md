GPU and CPU are running at the same time. CPU timing is only semi-accurate when you force sequential operation of the GPU and CPU. As this is not what we want in practice, it's a poor solution.

The GPU, by default, operates in a synchronous mode in that the memcpy operations implicitly synchronize. The programmer expects to copy to the device, run the kernel, copy back from the device, and have the results in memory to save to disk or for further processing. While this is an easy model to understand, it's also a slow model. It's one aimed at getting kernels to work, but not one aimed at performance.

We examined the use of streams, in detail, in Chapter 8. A stream is effectively a work queue. Stream 0 is used as the default work queue when you do not specify a stream to the CUDA API. However, stream 0 has many operations that implicitly synchronize with the host. You might be expecting an asynchronous operation, but in practice certain API calls have implicit synchronization when using stream 0.

To use asynchronous operations, we need to first create a stream such as

```
// Create a new stream on the device
cudaStream_t stream;
CUDA_CALL(cudaStreamCreate(&stream));
```

For the bandwidth test, we created an array of events.

```
#define MAX_NUM_TESTS 16
cudaEvent_t kernel_start[MAX_NUM_TESTS];
cudaEvent_t kernel_stop[MAX_NUM_TESTS];
```

The GPU provides events that can be time-stamped by the GPU hardware (Figure 9.24). Thus, to time a particular action on the GPU, you need to push a start event into the queue, then the action you wish to time, and finally a stop event. Streams are simply a FIFO (first in, first out) queue of operations for the GPU to perform. Each stream represents an independent queue of operations.

Having created a stream, you need to create one or more events.

```
for (u32 test=0; test < MAX_NUM_TESTS; test++)
{
    CUDA_CALL(cudaEventCreate(&kernel_start[test]));
    CUDA_CALL(cudaEventCreate(&kernel_stop[test]));
}
```

Here we have a simple loop creating MAX_NUM_TESTS events—a start event and a stop event. We then need to push the events into the stream on either side of the action to measure.

```
// Start event
CUDA_CALL(cudaEventRecord(kernel_start[test],stream));
```

```
// Run the kernel
```

| Start Event | Action to be timed | Stop Event |
|---|---|---|
| | | |
Time -->

**FIGURE 9.24** Timing an action on the GPU.