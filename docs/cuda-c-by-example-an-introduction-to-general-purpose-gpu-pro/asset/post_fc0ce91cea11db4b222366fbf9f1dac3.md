
```cpp
// allocate page-locked memory, used to stream
HANDLE_ERROR( cudaHostAlloc( (void**)&host_a,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&host_b,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&host_c,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
for (int i=0; i<FULL_DATA_SIZE; i++) {
    host_a[i] = rand();
    host_b[i] = rand();
}
```

We have allocated our input and output buffers on both the GPU and the host. Notice that we’ve decided to use pinned memory on the host by using cudaHostAlloc() to perform the allocations. There is a very good reason for using pinned memory, and it’s not strictly because it makes copies faster. We’ll see in detail momentarily, but we will be using a new kind of cudaMemcpy() function, and this new function requires that the host memory be page-locked. After allocating the input buffers, we fill the host allocations with random integers using the C library call rand().

With our stream and our timing events created and our device and host buffers allocated, we’re ready to perform some computations! Typically we blast through this stage by copying the two input buffers to the GPU, launching our kernel, and copying the output buffer back to the host. We will follow this pattern again, but this time with some small changes.

First, we will opt not to copy the input buffers in their entirety to the GPU. Rather, we will split our inputs into smaller chunks and perform the three-step process on each chunk. That is, we will take some fraction of the input buffers, copy them to the GPU, execute our kernel on that fraction of the buffers, and copy the resulting fraction of the output buffer back to the host. Imagine that we need to do this because our GPU has much less memory than our host does, so the computation needs to be staged in chunks because the entire buffer can't fit on the GPU at once. The code to perform this “chunkified” sequence of computations will look like this:

```cpp
// now loop over full data, in bite-sized chunks
for (int i=0; i<FULL_DATA_SIZE; i+=N) {
    // copy the locked memory to the device, async
    HANDLE_ERROR( cudaMemcpyAsync( dev_a, host_a+i,
                                   N * sizeof(int),
                                   cudaMemcpyHostToDevice,
                                   stream ) );
    HANDLE_ERROR( cudaMemcpyAsync( dev_b, host_b+i,
                                   N * sizeof(int),
                                   cudaMemcpyHostToDevice,
                                   stream ) );

    kernel<<<N/256, 256, 0, stream>>>( dev_a, dev_b, dev_c );

    // copy the data from device to locked memory
    HANDLE_ERROR( cudaMemcpyAsync( host_c+i, dev_c,
                                   N * sizeof(int),
                                   cudaMemcpyDeviceToHost,
                                   stream ) );
}
```

But you will notice two other unexpected shifts from the norm in the preceding excerpt. First, instead of using the familiar cudaMemcpy(), we're copying the data to and from the GPU with a new routine, cudaMemcpyAsync(). The difference between these functions is subtle yet significant. The original cudaMemcpy() behaves like the C library function memcpy(). Specifically, this function executes synchronously, meaning that when the function returns, the copy has completed, and the output buffer now contains the contents that were supposed to be copied into it.

The opposite of a *synchronous* function is an *asynchronous* function, which inspired the name `cudaMemcpyAsync()`. The call to `cudaMemcpyAsync()` simply places a *request* to perform a memory copy into the stream specified by the argument `stream`. When the call returns, there is no guarantee that the copy has even started yet, much less that it has finished. The guarantee that we have is that the copy will definitely be performed before the next operation placed into the same stream. It is required that any host memory pointers passed to `cudaMemcpyAsync()` have been allocated by `cudaHostAlloc()`. That is, you are only allowed to schedule asynchronous copies to or from page-locked memory.

Notice that the angle-bracketed kernel launch also takes an optional stream argument. This kernel launch is asynchronous, just like the preceding two memory copies to the GPU and the trailing memory copy back from the GPU. Technically, we can end an iteration of this loop without having actually started any of the memory copies or kernel execution. As we mentioned, all that we are guaranteed is that the first copy placed into the stream will execute before the second copy. Moreover, the second copy will complete before the kernel starts, and the kernel will complete before the third copy starts. So as we’ve mentioned earlier in this chapter, a stream acts just like an ordered queue of work for the GPU to perform.

When the `for` loop has terminated, there could still be quite a bit of work queued up for the GPU to finish. If we would like to guarantee that the GPU is done with its computations and memory copies, we need to synchronize it with the host. That is, we basically want to tell the host to sit around and wait for the GPU to finish before proceeding. We accomplish that by calling `cudaStreamSynchronize()` and specifying the stream that we want to wait for:

```cpp
// copy result chunk from locked to full buffer
HANDLE_ERROR( cudaStreamSynchronize( stream ) );
```

Since the computations and copies have completed after synchronizing stream with the host, we can stop our timer, collect our performance data, and free our input and output buffers.

```cpp
HANDLE_ERROR( cudaEventRecord( stop, 0 ) );

HANDLE_ERROR( cudaEventSynchronize( stop ) );
HANDLE_ERROR( cudaEventElapsedTime( &elapsedTime,
start, stop ) );
printf( "Time taken:  %3.1f ms\n", elapsedTime );

// cleanup the streams and memory
HANDLE_ERROR( cudaFreeHost( host_a ) );
HANDLE_ERROR( cudaFreeHost( host_b ) );
HANDLE_ERROR( cudaFreeHost( host_c ) );
HANDLE_ERROR( cudaFree( dev_a ) );
HANDLE_ERROR( cudaFree( dev_b ) );
HANDLE_ERROR( cudaFree( dev_c ) );
```

Finally, before exiting the application, we destroy the stream that we were using to queue the GPU operations.

```cpp
HANDLE_ERROR( cudaStreamDestroy( stream ) );
return 0;
}
```

To be honest, this example has done very little to demonstrate the power of streams. Of course, even using a single stream can help speed up an application if we have work we want to complete on the host while the GPU is busy churning through the work we've stuffed into a stream. But assuming that we don't have much to do on the host, we can still speed up applications by using streams, and in the next section we'll take a look at how this can be accomplished.

## 10.5 Using Multiple CUDA Streams

Let's adapt the single-stream example from Section 10.3: Using a Single CUDA Stream to perform its work in two different streams. At the beginning of the previous example, we checked that the device indeed supported overlap and broke the computation into chunks. The idea underlying the improved version of this application is simple and relies on two things: the “chunked” computation and the overlap of memory copies with kernel execution. We endeavor to get Stream 1 to copy its input buffers to the GPU while stream 0 is executing its kernel. Then stream 1 will execute its kernel while stream 0 copies its results to the host. Stream 1 will then copy its results to the host while stream 0 begins executing its kernel on the next chunk of data. Assuming that our memory copies and kernel executions take roughly the same amount of time, our application’s execution timeline might look something like Figure 10.1. The figure assumes that the GPU can perform a memory copy and a kernel execution at the same time, so empty boxes represent time when one stream is waiting to execute an operation that it cannot overlap with the other stream’s operation. Note also that calls to cudaMemcpyAsync() are abbreviated in the remaining figures in this chapter, represented simply as “memcpy.”

| Stream 0 | Stream 1 |
| :--- | :--- |
| memcpy A to GPU | |
| memcpy B to GPU | |
| kernel | memcpy A to GPU |
| | memcpy B to GPU |
| | kernel |
| memcpy C from GPU | memcpy C from GPU |
| | |
| memcpy A to GPU | |
| memcpy B to GPU | |
| kernel | memcpy A to GPU |
| | memcpy B to GPU |
| | kernel |
| memcpy C from GPU | memcpy C from GPU |

Figure 10.1 Timeline of intended application execution using two independent streams
