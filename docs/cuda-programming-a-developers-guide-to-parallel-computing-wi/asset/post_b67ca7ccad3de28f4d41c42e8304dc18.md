
do not want, and perhaps something later versions of the compiler may resolve. The LLVM compiler (CUDA 4.1) seems to prefer to place vector types into local memory rather than registers.

Finally, we moved the definition of round_num from the start of the function to just before the while loop and replaced its usage in round zero with an explicit zero index.

These steps brought the kernel register usage down from 43 registers to just 25 registers and dropped the execution time to just 4.32 ms, somewhat faster than the forced register allocation version. Forcing this to just 24 again resulted in slower code due to the compiler's usage of local memory. Unfortunately, we really want a maximum of 24 registers, not 25, as this will increase the block count and bring in another set of warps, increasing the overall amount of parallelism.

```
Let's replace
while (round_num <= num_rounds)
with
while (round_num <= NUM_ROUNDS)
```

This will eliminate the need to hold the formal parameter num_rounds in a register and allow the compiler to instead use a literal value of 10, the value of the #define for NUM_ROUNDS. Using a literal value serves two purposes. First, it allows the comparison of the register holding num_rounds with an immediate value, rather than a comparison of two registers. Second, it means the bounds of the loop are known, which in turn allows the compiler to safely unroll the entire loop or sections of the loop as needed.

This indeed allows the compiler to use just 24 registers, the magic boundary number we need to potentially schedule another block. The savings are significant, although with 256 threads per block we do not bring in any additional blocks. Despite this the time for 16 blocks does drop. However, the timing becomes erratic and quite variable, with some runs now taking longer than before. We're now starting to see the warps compete with one another. With such a small sample size (16 cipher blocks) the results become highly variable from run to run. Therefore, we'll increase the number of cipher blocks to 2048 K and average the results.

The strategy CUDA adopts when allocating registers is to try for the smallest number of registers possible. With our transition from 25 to 24 registers, using 256 threads per block, we can still only schedule two blocks. However, if we halve the number of threads per block, we can squeeze in another block of 128 threads. Thus, we can run five blocks per SM at 128 threads, 24 registers (640 total). This is compared with four blocks at 25 registers per block (512 threads). Does this make a difference? Yes, it does (see Table 7.3).

If we use a 64-thread version as a baseline, we hit the maximum limit of eight blocks, which in turn limits us to a total of 512 threads. The 128-thread version is limited to five blocks, 640 threads in total. The 256-thread version is limited to two blocks, again 512 threads total.

Table 7.3 Effect of Using Different Numbers of Threads

| 64 Threads | 128 Threads | 256 Threads |
| --- | --- | --- |
| 1150 ms | 1100 ms | 1220 ms |
| 100% | 96% | 111% |

You might expect the 64-thread version and the 256-thread version, given they both run a total of 512 threads, to take the same time. The 64-thread version is faster because it provides a better instruction mix, with different blocks performing different parts of the algorithm. The 256-thread version tends to have its threads all doing the same thing at the same time. Remember in this compute 1.2 device there is no L1/L2 cache, so this is simply a comparison of instruction and memory throughput. It’s also far easier for the CUDA runtime to get a better load balance between the two SMs due to the smaller scheduling unit.

Squeezing in that extra 64 threads by selecting a small number of threads per block gains us 120 ms, a 15% improvement over the 256-thread version on this compute 1.2 device. We can only do this because we are within the 24 register threshold.

With a small laptop ION-based GPU, we’re encoding around 1.8 million cipher blocks per second, which is approximately 28 MB/s including transfer times. Excluding the transfer times, this approximately doubles. This is the next area to address.

## Transfer performance

It’s necessary to transfer data to the GPU over the PCI-E data bus. Compared to access to memory, this bus is very slow. Chapter 9 explores in detail PCI-E transfer sizes and the effects of using paged or pinned memory. Pinned memory is memory that cannot be paged (swapped) out to disk by the virtual memory management of the OS. PCI-E transfer can, in fact, only be done using pinned memory, and if the application does not allocate pinned memory, the CUDA driver does this in the background for you. Unfortunately, this results in a needless copy operation from the regular (paged) memory to or from pinned memory. We can of course eliminate this by allocating pinned memory ourselves.

In the application, we simply replace the following lines when allocating memory in the host application:

```
uint4 * cipher_data_host = (uint4 *) malloc(size_of_cipher_data_in_bytes);
KEY_T * cipher_key_host = (KEY_T *) malloc(size_of_cipher_key_size_in_bytes);
```

with

```
uint4 * cipher_data_host;
KEY_T * cipher_key_host;
CUDA_CALL(cudaMallocHost(&cipher_data_host, size_of_cipher_data_in_bytes));
CUDA_CALL(cudaMallocHost(&cipher_key_host, size_of_cipher_key_size_in_bytes));
```

And at the end, when cleaning up the memory allocation on the host, we replace

```
free(cipher_key_host);
free(cipher_data_host);
```

with

```
CUDA_CALL(cudaFreeHost(cipher_data_host));
CUDA_CALL(cudaFreeHost(cipher_key_host));
```

So how does this affect performance? It reduces our 1100 ms time down to 1070 ms, a drop of some 30 ms, just a 3% decrease in the execution time. The actual gain is very dependent on the processor and chipset being used. Typically you see anything up to 20% performance gain in transfer time using this method. However, the laptop we are using for this test is using an X1 PCI-E 2.0 link. The fact that we see a minor but consistent improvement would suggest removing the redundant copy is significant in comparison to the actual copy time over this rather slow link.

Despite the miserable gain pinned memory has brought us on this platform, we need to use pinned memory for the next step in the optimization of the transfers.

## A single streaming version

We cover streams in detail in Chapter 8, as they are essential in using more than one GPU on a problem. We'll use them here in a single-GPU problem, as they allow us to both execute memory transfers and perform kernels at the same time. In effect, you must try to overlap the kernel execution with the transfer time. If we're lucky the transfer time is less than or equal to the calculation time. Thus, the transfer time is effectively hidden behind the compute time of a different stream and becomes free.

Streams are simply virtual work queues that we'll use here in a relatively simple manner. Initially we'll create a single stream and move from a synchronous operation to an asynchronous operation with respect to the CPU. With this approach we will likely see a slight improvement due to the decreased synchronization needed for an asynchronous operation, but I'd expect this to be minor. Only once you introduce multiple streams can you really expect to see any significant speedup.

Stream 0 is the default stream; the stream used if you do not specify one. This is a synchronous stream that helps significantly when debugging an application but is not the most efficient use of the GPU. Thus, we must first create an alternative stream. We then need to push the memory copy, events, and kernel operations into the stream.

The first thing we need to do is to create an alternative stream. This is done with

```
cudaStream_t aes_async_stream;
CUDA_CALL(cudaStreamCreate(aes_async_stream));
```

Conversely, we need to destroy the stream at the end of the host program once we're finished with it:

```
CUDA_CALL(cudaStreamDestroy(aes_async_stream));
```

Next, the copy and event operations need to have the new stream added. Thus, we change

```
// Copy to GPU and then zero host cipher memory
CUDA_CALL(cudaEventRecord(start_round_timer));
```

```
CUDA_CALL(cudaMemcpyAsync(cipher_data_device, cipher_data_host,
size_of_cipher_data_in_bytes, cudaMemcpyHostToDevice));
```

```
CUDA_CALL(cudaMemcpyAsync(cipher_key_device, cipher_key_host,
size_of_cipher_key_size_in_bytes, cudaMemcpyHostToDevice));
```

to

```
// Copy to GPU and then zero host cipher memory
CUDA_CALL(cudaEventRecord(start_round_timer, aes_async_stream));
```
