
```cpp
// record stop event on the default stream
cudaEventRecord(stop);
```

```cpp
// wait until the stop event completes
cudaEventSynchronize(stop);
```

```cpp
// calculate the elapsed time between two events
float time;
cudaEventElapsedTime(&time, start, stop);
```

```cpp
// clean up the two events
cudaEventDestroy(start);
cudaEventDestroy(stop);
```

the start and stop events are placed into the NULL stream by default. A timestamp is recorded for the start event at the beginning of the NULL stream, and a timestamp for the stop event at the end of the NULL stream. The elapsed time between the two events is then fetched using cudaEventElapsedTime.

# Stream Synchronization

Because all operations in non-default streams are non-blocking with respect to the host thread, you will run across situations where you need to synchronize the host with operations running in a stream.

From the host point of view, CUDA operations can be classified into two main categories:

- Memory-related operations
- Kernel launches

Kernel launches are always asynchronous with respect to the host. Many memory operations are inherently asynchronous (such as cudaMemcpy), but the CUDA runtime also provides functions for performing memory operations.

As you learned, there are two types of streams:

- Asynchronous streams (non-NULL streams)
- Synchronous streams (the NULL/default stream)

A non-null stream is an asynchronous stream with respect to the host; all operations opted to do not block host execution. On the other hand, the NULL-stream, declared implicitly, is a synchronous stream with respect to the host. Most operations opted to the NULL-stream cause the host to block on all preceding operations, the main exception being kernel launches.

Non-null streams can be further classified into the following types:

- Blocking streams
- Non-blocking streams

Even though non-NULL streams are non-blocking with respect to the host, operations within a non-NULL stream can be blocked by operations in the NULL stream. If a non-NULL stream is a blocking stream, the NULL stream can block operations in. If a non-NULL stream is a non-blocking stream, it will not block on operations on the NULL stream. In the following section, you will learn how to work with blocking and non-blocking streams.

# Blocking and Non-Blocking Streams

Streams created with cudaStreamCreate are blocking streams, meaning the execution of operations in those streams can be waited for by earlier operations in the NULL stream to complete. The NULL stream is an implicit stream, which synchronizes with all other blocking streams in the same CUDA context. In general, when an operation is issued to the NULL stream, the CUDA context waits on all operations previously issued to all blocking streams before starting that operation. Also, any operations issued to blocking streams will wait on pending operations in the NULL stream to complete before.

For example, the following code launches kernel_1 in stream_1, kernel_2 in the NULL stream, then kernel_3 in stream_2:

```cpp
kernel_1<<1, 0, stream_1>>>;
kernel_2<<1, 1>>>;
kernel_3<<1, 0, stream_2>>>;
```

The resulting behavior is that kernel_2 does not start executing on the GPU until kernel_1 completes, and kernel_3 does not start until kernel_2 completes. From the kernel's perspective, each kernel launch is still asynchronous and non-blocking.

The CUDA runtime provides a function that allows customization of a non-NULL stream's behavior in relation to the NULL stream:

```cpp
cudaError_t cudaStreamCreateFlags(cudaStream_t* pstream, unsigned int flags);
```

The flags argument determines the behavior of the created stream. Valid values for flags are:
cudaStreamDefault: default stream creation flag (blocking)
cudaStreamNonBlocking: asynchronous stream creation flag (non-blocking)

Specifying cudaStreamNonBlocking disables the behavior of non-NULL streams relative to the NULL stream. If stream_1 and stream_2 in the previous example were created with cudaStreamNonBlocking, none of the kernel executions would be blocked waiting for completion of any of the others.

# Implicit Synchronization

CUDA includes two types of device-host synchronization: explicit and implicit. You have already seen many functions that perform explicit synchronization, cudaDeviceSynchronize, cudaStreamSynchronize, and cudaEventSynchronize. These functions are explicitly called by the host to synchronize the execution of tasks on the device with the host thread. You manually insert explicit synchronization calls at logical points in your application.

You have already seen examples of implicit synchronization. For an example, cudaMemcpy implicitly synchronizes the device and host because the host application blocks until

```cpp
cudaError_t cudaEventSynchronize(cudaEvent_t event);
cudaError_t cudaEventQuery(cudaEvent_t event);
```

Additionally, cudaStreamWait offers a flexible way to introduce inter-stream dependencies using CUDA events:

```cpp
cudaError_t cudaStreamWait(cudaStream_t stream, cudaEvent_t event);
```

cudaStreamWait causes the specified stream to wait on the specified event before executing any operations queued after the call to cudaStreamWait. The event may be associated with either the same stream, or a different stream. In the latter case, this function performs cross-stream synchronization, as illustrated in Figure 6-4. Here, the wait issued by stream 2 ensures that the event created in stream 1 is satisfied before continuing.

![](img/506ba3a4c9f4512233692f3f20de1f3a_305_0.png)

FIGURE 6-4

# Configurable Events

The CUDA runtime provides a way to customize the behavior and properties of events:

```cpp
cudaError_t cudaEventCreateWithFlags(cudaEvent_t* event, unsigned int flags);
```

Valid flags include:

- cudaEventDefault
- cudaEventBlockingSync
- cudaEventDisableTiming
- cudaEventInterprocess

The flag cudaEventBlockingSync specifies that synchronizing with this event will block the call. The default behavior of cudaEventSynchronize is to spin on the event, using CPU cycles to constantly check the event's status. With cudaEventBlockingSync set, the thread gives up the core until the event is satisfied. While this can lead to fewer wasted CPU cycles or process by going to sleep if other useful work can be done, it can also lead to longer latencies between an event being satisfied and the calling thread being activated.

Passing cudaEventDisableTiming indicates that the created event is only used for synchronization and does not need to record timing data. Removing the overhead of taking timestamps improves the performance of calls to cudaStreamWaitEvent and cudaEventQuery.

The flag cudaEventInterprocess indicates that the created event may be used as an inter-process event.

# CONCURRENT KERNEL EXECUTION

Now that the concepts and APIs for streams, events, and synchronization have been explained, it is time to experiment using several examples. The first example shows how to run multiple kernels concurrently using multiple streams. This simple example will demonstrate several essential issues concerning concurrent kernel execution:

- Dispatching jobs with the depth-first or breadth-first approach
- Adjusting hardware work queues
- Avoiding false dependencies on Kepler and Fermi devices
- Adding the blocking behavior of the non-default stream
- Adding dependencies between non-default streams
- Examining how resource usage affects concurrency

# Concurrent Kernels in Non-NULL Streams

In this section, you will use the NVIDIA Visual Profiler nvvp to visualize kernel executions. The kernel used in this example contains dummy computation to simulate work execution on the device. This ensures that kernels are resident on the GPU for a long period of time so the overlap is apparent in the Visual Profiler. Note that this example uses identical kernels kernel_1, kernel_2, ...

```cpp
global void kernel_1() {
    double sum = 0.0;
    for (int i = 0; i < N; i++) {
        sum = sum + tan(0.1);
    }
}
```

This is done to make it easier to visualize the execution of different kernels in nvvp.
A set of non-null streams must be created first. Kernel launches each of these streams should run concurrently on the GPU, provided there are no false dependencies due to hardware resource limits.

```cpp
cudaStream_t *streams = (cudaStream_t*)malloc(n_streams * sizeof(cudaStream_t));
for (int i = 0; i < n_streams; i++) {
    cudaStreamCreate(&streams[i]);
}
```

Kernels can be dispatched in each of these streams using a loop to iterate over streams:

```cpp
dim3 block(1);
dim3 grid(1);
for (int i = 0; i < n_streams; i++) {
    kernel_1<<<grid, block, 0, streams[i]>>>();
    kernel_2<<<grid, block, 0, streams[i]>>>()();
}
```
