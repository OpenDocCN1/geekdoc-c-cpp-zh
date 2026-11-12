To use this feature under Windows 7 you need the 64-bit OS plus the TCC (Tesla compute cluster) drivers active. As the TCC driver will only activate with Tesla cards, effectively there is no mainstream consumer support for this in Windows 7. Thus, this should be considered as a feature suitable for clusters, high-performance computing (HPC), and other compute-centered applications. It's not something you can exploit with, say, a video transcoding application for consumer PCs.

To support P2P first you should check UVA is enabled:

```
struct cudaDeviceProp prop;
CUDA_CALL(cudaGetDeviceProperties(&device_prop));
if (device_prop.unifiedAddressing == 1) // If unified addressing is enabled
```

UVA will only be enabled under a 64-bit OS, or Windows 7 using the TCC driver.

Next you need to check if device A can talk to device B. Note, just because this test passes, it does not imply that device B can talk to device A. Resources are consumed in enabling P2P access in a given direction.

This test can be performed with the following code:

```
int peer_access_avail;
int src_device = 0;
int peer_device = 1;
CUDA_CALL(cudaDeviceCanAccessPeer( &peer_access_avail, src_device, peer_device));
if (peer_access_avail == 1) // If peer access from device 0 to device 1 is available
{
    int flags = 0;
    CUDA_CALL(cudaSetDevice(peer_device));
    CUDA_CALL(cudaEnablePeerAccess(peer_device, flags));
}
```

Once peer access has been enabled, memory can be accessed, in the direction of the peer access, either in device kernels or as host-initiated memory copies. Thus, device 0 can enable peer access to device 1, as in the previous example. You can then call a kernel on device 1, passing it a pointer to the global memory space from device 0. The kernel will then dereference this pointer in the same way as it would a zero-copy device pointer to host memory. Every time there is an access through that pointer device 1 will initiate a fetch over the PCI-E bus from device 0. Of course, the same caveats apply as with zero-copy memory usage, specifically that you should avoid re-reading such memory and try to achieve coalesced access patterns for performance reasons.

You can of course use such features for device-initiated memory copies. To do this from the device, have a device kernel fetch the data via a device pointer, and simply store it to the local device's global memory. Equally you can push as well as pull data from one device to another. However, if you want bidirectional access, you will need to remember to enable P2P access in both directions.

The second approach is an explicit memory copy, something we must initiate from the host. There are the two standard forms of this, the synchronous version and the asynchronous streamed version:

```
cudaMemcpyPeer(dst_device_ptr, dst_device_num, src_device_ptr,
src_device_num,num_bytes);
```