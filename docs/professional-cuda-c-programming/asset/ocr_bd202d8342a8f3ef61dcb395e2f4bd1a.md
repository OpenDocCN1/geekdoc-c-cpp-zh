memory model points-of-view. You have developed your ability to assist and analyze your kernel's behavior using the command-line profiler.

This chapter will examine grid level concurrency. In grid level concurrency, multiple kernel launches are executed simultaneously on a single device, often leading to better device utilization. In this chapter, you will learn how to use CUDA to implement grid level concurrency. You will also use the CUDA Visual Profiler NVP to visualize concurrent kernel execution.

# INTRODUCING STREAMS AND EVENTS

A CUDA stream refers to a sequence of asynchronous CUDA operations that execute on a device in the order issued by the host code. A stream encapsulates these operations, maintains their ordering, permits to be queued in the stream to be executed after all preceding operations, and allows for querying the status of queued operations. These operations can include host-device transfer, kernel launches, and other commands that are issued by the host but handled by the device. The execution of an operation in a stream is always asynchronous with respect to the host. The CUDA runtime determines when operation is eligible for execution on the device. It is your responsibility to use CUDA APIs to ensure an asynchronous operation has completed before using the result. While operations within the same CUDA stream have a strict ordering, operations in different streams have no restriction on order. By using streams to launch multiple simultaneous kernels, you can implement grid level concurrency.

Because all operations queued in a CUDA stream are asynchronous, it is possible to overlap their execution with other operations in the host-device system. By doing so you can hide the cost of performing operations performing other useful work at the same time.

Throughout this book, a typical pattern in CUDA programming has been:

+   1. Move input data from the host to the device.
2. Execute a kernel on the device.
3. Move the result from the device back to the host.

In many cases, more time is spent executing the kernel than transferring data. In these situations, you may be able to completely hide CPU-GPU communication latency. By dispatching kernel execution and data transfer into separate streams, these operations can be overlapped, and the total elapsed time is near the granularity of CUDA API calls. Streams can be used to implement pipelining or double buffering at the.

The functions in the CUDA API can be generally classified as either synchronous or asynchronous. Functions with synchronous behavior block the thread until they complete. Functions with asynchronous behavior return control to the host immediately after being called. Asynchronous functions and streams are the two basic pillars on which you can build grid-level concurrency in CUDA.

While a software point of view CUDA operations in different streams run concurrently; that may not be the case on physical hardware. Depending on PCIe bus contention or the availability of Per-SM resources, different CUDA streams still need to wait for each other in order to complete.