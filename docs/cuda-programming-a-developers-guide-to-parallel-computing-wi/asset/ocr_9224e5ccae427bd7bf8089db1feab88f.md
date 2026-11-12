```
// Create a device array and populate it with the host values
// A PCI-E transfer to device happens here
printf("Transferring to device");
thrust::device_vector<int> device_array = host_array;

// Sort the array on the device
printf("Sorting on device");
thrust::sort(device_array.begin(), device_array.end());

// Sort the array on the host
printf("Sorting on host");
thrust::sort(host_array.begin(), host_array.end());

// Create a host array and populate it with the sorted device values
// A PCI-E transfer from the device happens here
printf("Transferring back to host");
thrust::host_vector<int> host_array_sorted = device_array;

printf("Sorting Complete");

return 0;
}
```

# Problems with Thrust

What is interesting to note here is that the GPU- and CPU-based sorts may or may not be performed at the same time, depending on how you arrange the transfers. Unfortunately, Thrust always uses the default stream and you cannot change this as with NPP library. There is no stream parameter to pass, or function to set the currently selected stream.

Using the default stream has some serious implications. The sort operation is actually just a series of kernels run in stream 0. Kernels, like regular kernels, launch asynchronously. However, memory transfers, unless explicitly done asynchronously, operate synchronously. Thus, any function you call from Thrust that returns a value, reduce for example, and any copy back to the host causes an implicit synchronization. In the example code, placing the sort host array call after the copy back from the device code would have serialized the GPU and CPU sorts.

# Multi-CPU/GPU considerations

On the CPU side, Thrust automatically spawns N threads where N is the number of physical processor cores. Thrust is actually using OpenMP for the CPU side, and by default OpenMP will use the number of physical cores on the CPU.

It would be nice if the GPU version did this also, splitting the task over N GPUs. The host side implements a NUMA (nonuniform memory access)-based memory system. This means all memory addresses are accessible to any CPU socket and any CPU core. Thus, even on a dual-CPU system, 8, 12, or 16 CPU cores can work in parallel on a problem.