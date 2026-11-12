
![](img/d5750f02645080d2a91292047fbe0f98_226_0.png)

Figure 10.2 Mapping of CUDA streams onto GPU engines

![](img/d5750f02645080d2a91292047fbe0f98_227_0.png)

Figure 10.3 Arrows depicting the dependency of cudaMemcpyAsync() calls on kernel executions in the example from Section 10.4: Using Multiple CUDA Streams

![](img/d5750f02645080d2a91292047fbe0f98_228_0.png)

Figure 10.4 Execution timeline of the example from Section 10.4: Using Multiple CUDA Streams

The moral of this story is that we as programmers need to help out when it comes to ensuring that independent streams actually get executed in parallel. Keeping in mind that the hardware has independent engines that handle memory copies and kernel executions, we need to remain aware that the order in which we enqueue these operations in our streams will affect the way in which the CUDA driver schedules these for execution. In the next section, we’ll see how to help the hardware achieve overlap of memory copies and kernel execution.

## 10.7 Using Multiple CUDA Streams Effectively

As we saw in the previous section, if we schedule all of a particular stream’s operations at once, it’s very easy to inadvertently block the copies or kernel executions of another stream. To alleviate this problem, it suffices to enqueue our operations breadth-first across streams rather than depth-first. That is, rather than add the copy of a, copy of b, kernel execution, and copy of c to stream 0 before starting to schedule on stream 1, we bounce back and forth between the streams assigning work. We add the copy of a to stream 0, and then we add the copy of a to stream 1. Then we add the copy of b to stream 0, and then we add the copy of b to stream 1. We enqueue the kernel invocation in stream 0, and then we enqueue one in stream 1. Finally, we enqueue the copy of c back to the host in stream 0 followed by the copy of c in stream 1.

To make this more concrete, let's take a look at the code. All we've changed is the order in which operations get assigned to each of our two streams, so this will be strictly a copy-and-paste optimization. Everything else in the application will remain unchanged, which means that our improvements are localized to the For () loop. The new, breadth-first assignment to the two streams looks like this:

```
for (int i=0; i<FULL_DATA_SIZE; i+=N*2) {
    // enqueue copies of a in stream0 and stream1
    HANDLE_ERROR( cudaMemcpyAsync( dev_a0, host_a+i,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream0 ) );
    HANDLE_ERROR( cudaMemcpyAsync( dev_a1, host_a+i+N,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream1 ) );
    // enqueue copies of b in stream0 and stream1
    HANDLE_ERROR( cudaMemcpyAsync( dev_b0, host_b+i,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream0 ) );
    HANDLE_ERROR( cudaMemcpyAsync( dev_b1, host_b+i+N,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream1 ) );
    // enqueue kernels in stream0 and stream1
    kernel<<<N/256,256,0,stream0>>>( dev_a0, dev_b0, dev_c0 );
    kernel<<<N/256,256,0,stream1>>>( dev_a1, dev_b1, dev_c1 );
}
```

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

![](img/d5750f02645080d2a91292047fbe0f98_230_0.png)

## 10.8 Chapter Review

In this chapter, we looked at a method for achieving a kind of task-level parallelism in CUDA C applications. By using two (or more) CUDA streams, we can allow the GPU to simultaneously execute a kernel while performing a copy between the host and GPU. We need to be careful about two things when we endeavor to do this, though. First, the host memory involved needs to be allocated using `cudaHostAlloc()` since we will queue our memory copies with `cudaMemcpyAsync()`, and asynchronous copies need to be performed with pinned buffers. Second, we need to be aware that the order in which we add operations to our streams will affect our capacity to achieve overlapping of copies and kernel executions. The general guideline involves a breadth-first, or round-robin, assignment of work to the streams you intend to use. This can be counterintuitive if you don't understand how the hardware queuing works, so it's a good thing to remember when you go about writing your own applications.

This page intentionally left blank

# Chapter 11

# CUDA C on Multiple GPUs

There is an old saying that goes something like this: “The only thing better than computing on a GPU is computing on two GPUs.” Systems containing multiple graphics processors have become more and more common in recent years. Of course, in some ways multi-GPU systems are similar to multi-CPU systems in that they are still far from the common system configuration, but it has gotten quite easy to end up with more than one GPU in your system. Products such as the GeForce GTX 295 contain two GPUs on a single card. NVIDIA’s Tesla S1070 contains a whopping four CUDA-capable graphics processors in it. Systems built around a recent NVIDIA chipset will have an integrated, CUDA-capable GPU on the motherboard. Adding a discrete NVIDIA GPU in one of the PCI Express slots will make this system multi-GPU. Neither of these scenarios is very farfetched, so we would be best served by learning to exploit the resources of a system with multiple GPUs in it.

## 11.1 Chapter Objectives

Through the course of this chapter, you will accomplish the following:

- You will learn how to allocate and use zero-copy memory.
- You will learn how to use multiple GPUs within the same application.
- You will learn how to allocate and use portable pinned memory.

## 11.2 Zero-Copy Host Memory

In Chapter 10, we examined pinned or page-locked memory, a new type of host memory that came with the guarantee that the buffer would never be swapped out of physical memory. If you recall, we allocated this memory by making a call to cudaHostAlloc() and passing cudaHostAllocDefault to get default, pinned memory. We promised that in the next chapter, you would see other more exciting means by which you can allocate pinned memory. Assuming that this is the only reason you’ve continued reading, you will be glad to know that the wait is over. The flag cudaHostAllocMapped can be passed instead of cudaHostAllocDefault. The host memory allocated using cudaHostAllocMapped is pinned in the same sense that memory allocated with cudaHostAllocDefault is pinned, specifically that it cannot be paged out or relocated within physical memory. But in addition to using this memory from the host for memory copies to and from the GPU, this new kind of host memory allows us to violate one of the first rules we presented in Chapter 3 concerning host memory: We can access this host memory directly from within CUDA C kernels. Because this memory does not require copies to and from the GPU, we refer to it as zero-copy memory.

### 11.2.1 ZERO-COPY DOT PRODUCT

Typically, our GPU accesses only GPU memory, and our CPU accesses only host memory. But in some circumstances, it’s better to break these rules. To see an instance where it’s better to have the GPU manipulate host memory, we’ll revisit our favorite reduction: the vector dot product. If you’ve managed to read this entire book, you may recall our first attempt at the dot product. We copied the two input vectors to the GPU, performed the computation, copied the intermediate results back to the host, and completed the computation on the CPU.
