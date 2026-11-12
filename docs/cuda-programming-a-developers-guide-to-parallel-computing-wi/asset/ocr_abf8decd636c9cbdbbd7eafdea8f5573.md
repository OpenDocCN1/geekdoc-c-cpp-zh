You might expect the 64-thread version and the 256-thread version, given they both run a total of 512 threads, to take the same time. The 64-thread version is faster because it provides a better instruction mix, with different blocks performing different parts of the algorithm. The 256-thread version tends to have its threads all doing the same thing at the same time. Remember in this compute 1.2 device there is no L1/L2 cache, so this is simply a comparison of instruction and memory throughput. It’s also far easier for the CUDA runtime to get a better load balance between the two SMs due to the smaller scheduling unit.

Squeezing in that extra 64 threads by selecting a small number of threads per block gains us 120 ms, a 15% improvement over the 256-thread version on this compute 1.2 device. We can only do this because we are within the 24 register threshold.

With a small laptop ION-based GPU, we’re encoding around 1.8 million cipher blocks per second, which is approximately 28 MB/s including transfer times. Excluding the transfer times, this approximately doubles. This is the next area to address.

# Transfer performance

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

So how does this affect performance? It reduces our 1100 ms time down to 1070 ms, a drop of some 30 ms, just a 3% decrease in the execution time. The actual gain is very dependent on the processor and