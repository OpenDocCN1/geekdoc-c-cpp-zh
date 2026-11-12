
```c
void memcpy_test_zero_to_from(const int device_num,
                              const size_t size_in_bytes,
                              TIMER_T * const kernel_time,
                              const u32 num_runs,
                              const bool pinned)
{
    char device_prefix[256];
    int major, minor;
    int zero_copy_supported;

    // Init

    // Enable host mapping to device memory
    CUDA_CALL(cudaSetDeviceFlags(cudaDeviceMapHost));

    // Get the device properties
    get_device_props(device_prefix, device_num, &major,
                     &minor, &zero_copy_supported);

    // Exit if zero copy not supported and is requested
    // (zero_copy_supported == 0)
    if (!zero_copy_supported)
    {
        printf("*%s Error Zero Copy not supported", device_prefix);
        wait_exit(1);
    }

    // Select the specified device
    CUDA_CALL(cudaSetDevice(device_num));

    printf("*%s Running Memcpy Test to device using", device_prefix);

    if (pinned)
        printf("* locked memory*");
    else
        printf("* unlocked memory*");

    printf("* %lu K", size_in_bytes / 1024);

    (*kernel_time) = 0;

    init_device_timer();

    // Allocate data space on GPU
    u32 * gpu_data;
    CUDA_CALL(cudaMalloc((void**)&gpu_data,
                         size_in_bytes));

    u32 * dev_host_data_to_device;
    u32 * dev_host_data_from_device;
    // Allocate data space on host
    u32 * host_data_to_device;
    u32 * host_data_from_device;

    if (pinned)
    {
    // Allocate zero copy pinned memory
    CUDA_CALL(cudaHostAlloc((void **) &host_data_to_device, size_in_bytes,
    cudaHostAllocWriteCombined | cudaHostAllocMapped));
    CUDA_CALL(cudaHostAlloc((void **) &host_data_from_device, size_in_bytes,
    cudaHostAllocDefault | cudaHostAllocMapped));
    }
    else
    {
    host_data_to_device = (u32 *) malloc(size_in_bytes);
    host_data_from_device = (u32 *) malloc(size_in_bytes);
    }

    // Convert to a GPU host pointer
    CUDA_CALL(cudaHostGetDevicePointer(&dev_host_data_to_device, host_data_to_device, 0));
    CUDA_CALL(cudaHostGetDevicePointer(&dev_host_data_from_device, host_data_from_device,
    0));

    // If the host allocation did not result in
    // an out of memory error
    if ( (host_data_to_device != NULL) &&
    (host_data_from_device != NULL) )
    {
    const int num_elements = (size_in_bytes / sizeof(u32));
    const int num_threads = 256;
    const int num_grid = 64;
    const int num_blocks = (num_elements + (num_threads-1)) / num_threads;
    int num_blocks_per_grid;
    // Split blocks into grid
    if (num_blocks > num_grid)
    num_blocks_per_grid = num_blocks / num_grid;
    else
    num_blocks_per_grid = 1;
    dim3 blocks(num_grid, num_blocks_per_grid);
    for (u32 test=0; test < num_runs+1; test++)
    {
    // Add in all but first test run
    if (test == 0)
        start_device_timer();

    // Run the kernel
    kernel_copy<<<blocks, num_threads>>>(dev_host_data_to_device,
        dev_host_data_to_device, num_elements);

    // Wait for device to complete all work
    CUDA_CALL(cudaDeviceSynchronize());

    // Check for kernel errors
    cuda_error_check(device_prefix, " calling kernel kernel_copy");

    // Add in all but first test run
    if (test == 0)
        (*kernel_time) += stop_device_timer();
    }

    // Average over number of test runs
    (*kernel_time) /= num_runs;

    if (pinned)
    {
        // Free pinned memory
        CUDA_CALL(cudaFreeHost(host_data_to_device));
        CUDA_CALL(cudaFreeHost(host_data_from_device));
    }
    else
    {
        // Free regular paged memory
        free(host_data_to_device);
        free(host_data_from_device);
    }

    CUDA_CALL(cudaFree(gpu_data));
    destroy_device_timer();

    // Free up the device
    CUDA_CALL(cudaDeviceReset());

    printf(" KERNEL:%2.2f ms ", (*kernel_time));

    const float one_mb = (1024 * 1024);
    const float kernel_time_for_one_mb = (*kernel_time) * (one_mb / size_in_bytes);

    // Adjust for doing a copy to and back
    const float MB_per_sec = ((1000.0F / kernel_time_for_one_mb) * 2.0F);
    printf(" KERNEL:%f MB/s", MB_per_sec );
    }
}
```

## Bandwidth limitations

The ultimate bandwidth limitation of a significant number of applications is the I/O speed of whatever devices the input and output data have to be acquired from and written to. This is often the limitation on the speedup of any application. If your application takes 20 minutes to run on a serial CPU implementation and can express enough parallelism, it’s quite feasible for that application to run on a GPU in less time than it takes to load and save the data from the storage device you are using.

The first problem we have in terms of bandwidth is simply getting the data in and out of the machine. If you are using network-attached storage, the limit to this will be the speed of the network link. The best solution to this problem is a high-speed SATA3 RAID controller using many high-speed SSD drives. However, this will not solve your bandwidth issues unless you are using the drive efficiently. Each drive will have a peak transfer rate into host memory, which is actually a function of the transfer rate of the drive, the controller, and the route to host memory.

Running a benchmark on a drive, such as the commonly used ATTO benchmark, can show you the effect of using different size blocks (see Figure 9.20). This benchmark simulates access to drives based on a certain size of reads and writes. Thus, it reads and writes a 2 GB file in blocks of 1 K, 2 K, 4 K, etc. to see the effect of changing the block size.

We can see from the results that only when we read data in 64 K chunks or more do we achieve the peak bandwidth from the single SSD drive. For the RAID 0 hard drive system we need at least 1 MB blocks to make use of the multiple disks. Thus, you need to make sure you're using the `fread` function

![](img/e0b192dbaf05f61ad420bee512a8c4e4_361_0.png)

**FIGURE 9.20**
Bandwidth (MB/s) for a single SSD versus five hard disks in RAID 0.

in C to read suitable sized blocks of data from the disk subsystem. If we fetch data in 1 K chunks, we get just 24 MB/s from the drive, less than 10% of its peak read bandwidth. The more drives you add to a RAID system, the larger the minimum block size becomes. If you are processing compressed music or image files, the size of a single file may only be a few megabytes.

Note also that whether the data is compressible or not has a big impact on drive performance. The server level drives, such as the OCZ Vertex 3, provide both higher peak values and sustained bandwidth with uncompressible data. Thus, if your dataset is in an already compressed format (MP3, MP4, WMV, H.264, JPG, etc.), then you need to make sure you use server drives. The bandwidth on many consumer level SSD drives can fall to half of quoted peak when using uncompressible data streams.

The reason for this is the use of synchronous NAND memory in the high-end server SSDs versus the cheaper and much lower-performing asynchronous NAND memory used in consumer SSDs. Even with noncompressed data, synchronous NAND-based drives still outperform their asynchronous cousins, especially once the drive starts to contain some data. OCZ also provides the RevoDrive R4 PCI-E-based product, which claims speeds in the order of 2 GB/s plus at the expense of a PCI-E slot.

The next bandwidth limit you hit is that of host memory speed. This is typically not an issue until you introduce multiple GPUs per node, if you consider that you can fetch data at 6 GB/s off the PCI-E bus from a very high-speed SSD RAID system. We then have to send out data at 6 GB/s to and from the host memory to the GPU. Potentially you could also write data again at 6 GB/s to the RAID controller. That's a potential 24 GB/s of pure data movement without the CPU actually doing anything useful except moving data. We're already hitting the bandwidth limits of most modern processor designs and have already surpassed that available from the older-generation CPUs. In fact, only the latest quad channel i7 Sandybridge-E CPU has anything like the bandwidth we could start moving around, if we were to solve the slow I/O device issue.

CUDA 4.0 SDK introduced Peer2Peer GPU communication. The CUDA 4.1 SDK also introduced Peer2Peer communication with non-NVIDIA hardware. Thus, with the correct hardware, GPUs can talk to any supported device. This is mostly limited to a small number of InfiniBand and other high-speed network cards. However, in principle, any PCI-E device can talk with the GPU. Thus, a RAID controller could send data directly to and from a GPU. There is a huge potential for such devices, as no host memory bandwidth, PCI-E, or memory is consumed. As data is not having to flow to a CPU and then back out again, latency is dropped considerably.

Once the data has been moved out again to the GPU, there is a bandwidth limit of up to 190 GB/s on GeForce cards and 177 GB for Tesla, to and from the global memory on the device. To achieve this you need to ensure coalescing of the data reads from the threads and ensure your application makes use of 100% of the data moved from memory to the GPU.

Finally, we have shared memory. Even if you partition data into tiles, move it into shared memory, and access it in a bank conflict-free manner, the bandwidth limit is on the order of 1.3 TB/s. For comparison the AMD Phenom II and Nehalem i7 CPUs for a 64 KB L1 cache block, the same capacity as the GPU L1 cache and shared memory, has around 330 GB/s bandwidth, some 25% of that of the GPU.

If we take a typical float or integer parameter, it's 4 bytes wide. Thus, the bandwidth to global memory is a maximum of 47.5 giga-elements per second (190 GB/s ÷ 4). Assuming you read and write just one value, we can halve this figure to 23.75 giga-elements per second. Thus, with no data reuse, this is the maximum upper throughput of your application.
