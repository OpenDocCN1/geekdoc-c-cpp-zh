if kernels or transfers issued by the current thread are still executing on the current device, because cudaDevice does not cause host synchronization.

To recap, fetching the number of GPUs in a single node and the properties of those GPUs is possible using:

```
cudaError_t cudaDeviceCount(int *count);
cudaError_t cudaDeviceProperties(struct cudaDeviceProp *prop, int device);
```

You can then set the current device using:

```
cudaError_t cudaDeviceSet(int device);
```

Once the device is set, all CUDA operations are issued in the context of that. The selected device can then be used in the same way as you have been programming GPUs throughout this book.

# Peer-to-Peer Communication

Kernels executing in 64-bit applications on compute capability 2.0 and higher can directly access the global memory of any GPU connected to the same PCIe root node. To do so, you must use the CUDA peer-to-peer (P2P) API to enable direct-device communication. Peer-to-peer communication requires CUDA 4.0 or higher, the corresponding GPU drivers, and a system with two or more Fermi or Kepler GPUs connected to the same PCIe root node. There are two modes supported by CUDA P2P APIs that allow direct communication between GPUs:

+   - Peer-to-Peer Access: Direct load and store addresses within a CUDA kernel and across GPUs.
- Peer-to-Peer Transfer: Directly copy data between GPUs.

If two GPUs are connected to different PCIe root nodes within a system, then direct peer-to-peer access is not supported and the CUDA P2P API will inform you of that. You can still use the CUDA P2P API to perform peer-to-peer transfer between these devices, but the driver will transparent transfer data through host memory for these transactions rather than directly across the PCIe bus.

# Enabling Peer Access

Peer-to-peer access allows GPUs connected to the same PCIe root node to directly reference data stored in memory device other GPUs. Transparent to the kernel, the referenced data will be transferred over the PCIe bus to the requesting thread.

Because not all GPUs support peer-to-peer access, you need to explicitly check if a device supports P2P using the following function:

```
cudaError_t cudaDeviceCanAccessPeer(int* canAccessPeer, int device,
 int device);
```

This function returns an integer value of 1 in the variable canAccessPeer if the device device is able to directly access the global memory of peer device peerDevice; otherwise it returns a value of 0.