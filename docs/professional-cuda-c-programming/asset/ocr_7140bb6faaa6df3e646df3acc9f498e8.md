Combining the peer-to-peer CUDA APIs with UVA enables transparent access to memory on any device. You do not have to manually manage memory buffers or make explicit copies from host memory. The underlying system makes it possible to explicitly performing these operations and thus simplifies code. Note that relying too heavily on UVA to perform peer-to-peer accesses can have negative impacts, the overhead from many small transfers across the PCIe bus is significant.

The following code demonstrates how to check if a device supports addressing:

```
int deviceID = 0;
cudaGetDeviceProperties(&prop, deviceID);
printf("GPU%d: %s addressing\n", deviceID, prop.unifiedAddressing ? "does not support");
```

To use UVA, applications must be compiled on a 64-bit architecture with devices of compute capability 2.0 or higher, and CUDA 4.0 or later installed. If peer-to-peer access and UVA are both enabled, kernels can dereference a pointer to memory on another device.

You can use the simple kernel (which scales the input array by 2, and stores the results in an output array), to test peer-to-peer memory access from the GPU:

```
__global void kernel(float* src, float* dst) {
  const int idx = blockIdx.x * blockDim.x + threadIdx.x;
  dst[idx] = src[idx] * 2.0f;
}
```

The following code sets 0 as the current device and has the read global memory from device 1 using the pointer d_src[0], writing the result to the current device through the global memory pointer d_rcv[0]:

```
cudaSetDevice(0);
kernel<<<grid,block>>>(d_rcv[0], d_src[0]);
```

The following code sets 1 as the current device and has the read global memory from device 0 using the pointer d_src[0], writing the result to the current device through the global memory pointer d_rcv[1]:

```
cudaSetDevice(1);
kernel<<<grid,block>>>(d_rcv[1], d_src[0]);
```

These codes are included in the simple P2P_PingPong.cu. The following output indicates that these kernels ran successfully:

+   2. Running kernel on GPU1, taking source data from GPU0 and writing to GPU...
3. Running kernel on GPU0, taking source data from GPU1 and writing to GPU0...