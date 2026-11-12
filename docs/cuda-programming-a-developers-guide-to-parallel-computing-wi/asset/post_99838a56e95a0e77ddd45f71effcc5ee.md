
Atomic operations are used where we have many threads that need to write to a common output. They guarantee that the read/write/modify operation will be performed as an entire serial operation. They, however, do not guarantee any ordering of the read/write/modify operation. Thus, if both SM 0 and SM 1 ask to perform an atomic operation on the same address, which SM goes first is not defined.

Let's consider the classic parallel reduction algorithm. It can be viewed as a simple tree as shown in Figure 12.4. We have a number of ways to view this operation. We could allocate A, B, C, and D to a single thread and have those threads do an atomic add to an output storing (A,B) and (C,D). We then drop down to two threads, each of which would add the partial result to the final result.

Alternatively, we could start with the second line and use two threads. Thread 0 would read the contents of A and B and write it as the designated output address. Thread 1 would handle the inputs from C and D. Thread 1 would then drop out, leaving thread 0 to add the two partial results. Equally, we could reduce the problem to a single thread by simply having thread 0 calculate A + B + C + D.

The first approach works by considering the destination data writing to a common output, a scatter operation. The other approaches work by considering the source data and gathering it for use in the next stage. The scatter operation, because more than one contributor is writing to the output, requires the use of atomic operations. The gather approach completely eliminates the use of atomic operations and is therefore usually the preferable solution.

Atomic operations introduce serialization if, in fact, there is more than a single thread trying to perform a write at exactly the same time. If the writes are distributed in time such that there is no conflicting write, then an atomic operation has no significant cost. However, you cannot say with any certainty in a complex system that there will be absolutely no two writes happening at any single point in time. Therefore, even if writes are expected to be sparsely distributed in time, we need to use atomics to ensure this is always the case.

Given we can replace an atomic write with a gatherer operation, which does not need any form of data locking, does it make sense to use atomics at all? The answer in most cases is the gather approach will be quicker. However, this comes at a cost.

In our reduction example the addition of two numbers is trivial. Given just four numbers, we could easily eliminate all threads and have a single thread add the four numbers sequentially. This clearly

![](img/e0b192dbaf05f61ad420bee512a8c4e4_556_0.png)

FIGURE 12.4 Classic reduction.

| Number of Threads | Execution Time | % Time | Expected % | Overhead % |
|---|---|---|---|---|
| 1 | 5.78 | 100 | 100 | 0 |
| 2 | 3.05 | 53 | 50 | 3 |
| 3 | 2.12 | 37 | 33 | 4 |
| 4 | 1.71 | 30 | 25 | 5 |
| 5 | 1.52 | 26 | 20 | 6 |
| 6 | 1.46 | 25 | 17 | 8 |

works for trivial amounts of values, but what if we have 32 million values that we have to process in some form of reduction?

We saw in the reduction example from Chapter 9 that using a single thread on a CPU was slower than two threads, which itself was slower than three. There is a clear tradeoff here between the amount of work done by a given thread and the overall number of threads running. In the CPU case the maximum throughput on our AMD Phenom II 905e system was effectively limited to three threads due to memory bandwidth issues on the host.

A more modern processor, such as the Sandybridge-E, has higher host memory bandwidth, but at the same time, two additional processor cores (six instead of four). Running the same OpenMP reduction on a Sandybridge-E i7 3930 K system produces the results shown in Table 12.3 and Figure 12.5. Thus, even if we hugely increase the memory bandwidth and increase the core count, we see the same issue as before. Using more threads on CPU-based architecture produces progressively lower returns as we add more and more cores.

Running only two threads would not make use of the hardware. Running 16 million threads and killing half of them every reduction round would also not be a good approach on a CPU. On a GPU we could adopt this approach since the GPU creates a thread pool that gradually moves through the 32 million threads the programmer requested. We can, of course, manually create a similar thread pool on the CPU, although we have far fewer cores with which we can run threads.

![](img/e0b192dbaf05f61ad420bee512a8c4e4_557_0.png)

## FIGURE 12.5 OpenMP scaling on Sandybridge-E.

Our approach with the reduction example from Chapter 9 is a gather operation mixed with the scatter operation. We schedule a number of blocks based on a multiple of the number of SMs physically present on the device. We then divide the data set into N blocks and have each thread gather the necessary data from memory to perform a local, on-chip accumulation.

Each thread is doing a significant amount of work. We can see from the previous timing example that the wider data bus and double the number of SMs on the GTX470 allow it to complete this operation much quicker than the GTX460. We want to ensure we’re using the parallelism present in the device, be it a GPU or CPU, to the maximum.

Having calculated the partial sums on a per-thread basis, the issue then is how to combine the partial sums. This is where atomic operations become necessary because the accumulated data is private to the thread. Thus, it’s not possible to gather this data from another thread without the source thread writing its data somewhere.

A typical compute 2.0 GPU has up to 16 SMs, each of which can run up to 48 warps of 32 threads each. Thus, we have up to 24.5 K threads active at any point in time. Atomic operations can be performed in shared memory (from compute 1.1 devices and later) or in global memory. Shared memory atomics are, not surprisingly, significantly faster than having to go all the way out of the SM to global memory for global memory–based atomics. As we have up to 16 SMs, the shared memory–based atomics are 16 times wider than a write to global memory. Therefore, we want to use shared memory atomics wherever possible.

Atomic functions as a whole are only available on compute 1.1 devices, which is basically any device except the early GTX8800 series cards. 32-bit integer atomic operations on shared memory became available in compute 1.2 (the 9800 series and later). 64-bit integer atomic operations became available in global memory from compute 1.2 devices and in shared memory from compute 2.0 devices (the GTX400 series).

Single-precision, floating point–based atomic operations are available only in compute 2.0 and later. Double-precision atomics are not natively supported in any current hardware. However, you can implement them via software. The CUDA programming guide provides an example of how to do this using the atomic CAS (compare and swap) operation.

Understanding when to use gather operations and when to use scatter operations are often key to achieving both correctness and performance. Think about how best to structure the design to minimize the use of atomics (scatters) and maximize the use of gather operations instead.

## ALGORITHMIC ISSUES

The final type of problem programmers hit is a tricky one. The program runs and doesn’t produce any errors, but the answer is wrong.

### Back-to-back testing

Testing is something that is key to a programmer being perceived as either someone who writes “good code” or someone who throws together something that occasionally works. As a professional programmer you should strive to deliver the best-quality software you are able to in the timeframe available. How can you achieve this?

Back-to-back testing is a technique that acknowledges that it is much harder to write code that executes in parallel than a functionally equivalent set of code for a serial processor. With this in mind you always develop, in parallel or prior to the CUDA application, a serial implementation of the problem. You then run the identical dataset through both sets of code and compare the output. Any difference tells you that you may have an issue.

Now why do I only say “may” have an issue? The answer is largely down to if you are using floating-point (single- or double-precision) numbers or not. The issue with floating-point numbers is rounding and precision. Adding a large series of random floating-point numbers on a serial CPU from the lowest array value to the highest array value will result in a different value than if you were to add the same numbers from the highest array index to the lowest array index. Try it and see.

Now why is this? Single-precision, floating-point numbers use 24 bits to hold the mantissa value and 8 bits to hold the exponent. If we add 1.1e+38 to 0.1e−38 what do you think the result will be? The answer is 1.1e+38. The tiny value represented by 0.1e−38 is too small to be represented in the mantissa part. Over a large set of numbers there will be many of these types of issues. Therefore, the order in which the numbers are processed becomes important. To preserve accuracy often the best way to solve this issue is to sort the set of numbers and add from the lowest number to the largest. However, this introduces potentially a significant amount of work, in the terms of the sort, for this enhanced precision.

There are also other issues concerning the handling of floating-point values in compute 1.x devices, especially with very small numbers around 0, which may cause them to handle floating-point numbers in different ways than the same code running on the CPU. Thus, it’s often best to compromise and allow a certain threshold of error when dealing with floating-point equivalence tests.

If you have an existing CPU solution, then it is relatively simple to compare the results. With integer-based problems the standard C library function memcmp (memory compare) is quite sufficient to see if there is a difference between two sets of outputs. Usually when there is a programming error on the GPU side, the results are not just a little different, but greatly different, so it’s easy to say this code does or does not work and at which point in the output the difference occurs.

More difficult are aspects where the results match up until a certain point. Typically this might be the first 256 values. As 256 is often used as a thread count, this points to an error in the block index calculation. Only the first 32 values being correct points to an error in the thread index calculation.

Without an already existing CPU implementation, you’ll need to write one or use someone else’s implementation that you know works. However, actually writing your own serial implementation allows you to formulate the problem and understand it much better before attempting a parallel implementation. You have to, of course, ensure the serial version produces the expected answer before you start the parallel work.

It also provides a useful benchmark to see if using the GPU is providing a good speedup. In this evaluation always consider any transfer times for the PCI-E bus. As with the reduction example, we could write a reduction algorithm on the GPU that runs much faster than its CPU OpenMP equivalent. However, just sending the data to the GPU swamped any execution time saving. Be aware the GPU is not always the best solution. Having a CPU counterpart can let you evaluate this decision easily. The solution should be about maximizing the use of whatever resources are available, CPU and GPU.

Once the back-to-back test is set up, and there are many such examples where we do this in the various examples in this book, you can instantly see if you introduce an error. As you see this at the point you introduce it, it makes finding and identifying the error far easier. Combining this with
