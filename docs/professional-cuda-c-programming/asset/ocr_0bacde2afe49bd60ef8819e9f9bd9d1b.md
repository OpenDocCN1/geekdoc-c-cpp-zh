To help illustrate how CUDA streams are used in practice, the following is a common pattern for
dispatching CUDA operations to multiple streams.

```
for (int i = 0; i < nStreams; i++) {
    int offset = i * bytesPerStream; &[offset]
    cudaMemcpyAsync(&d_a[offset], bytePerStream, streams[i]);
    kernel<<<grid, block, 0, streams[i]>>>(d_a[offset]);
    cudaMemcpyAsync(&h_a[offset], d_a[offset], bytesPerStream, streams[i]);
}

for (int i = 0; i < nStreams; i++) {
    cudaStreamSynchronize(streams[i]);
}
```

Figure 6-1 illustrates a sample timeline of CUDA operations using three streams. Both data transfer\and kernel computation are evenly distributed among three concurrent streams.

| Serial | Memory Copy (H2D) | Kernel | Memory Copy (D2H) |
|---|---|---|---|
| Concurrent | H2D | K1 | D2H | |
| | H2D | K2 | D2H | Performance improvement |
| | | H2D | K3 | D2H |

FIGURE 6-1

You might notice that the data transfer operations are not executed concurrently in Figure 6-1, even
they are issued in separate streams. This contention is caused by a shared resource: the PCIe
bus. While these operations are independent from the point-of-view of the programming model,
bey they share a common hardware resource their execution must be serialized. Devices with a
double PCIe bus can overlap two data transfers, but they must be in different streams and in differ-
ent directions. In Figure 6-1, observe that data transfer from the host to the device in one stream is
onlinear with data transfer from the device to the host.

The maximum number of concurrent kernels is device-dependent. Fermi devices support 16-way
currency, and Kepler devices support 32-way concurrency. The number of concurrent kernels is
further limited by available compute resource on devices, such as shared memory and registers. You
will explore these through examples later in this chapter.

# # Stream Scheduling

Conceptually, all streams can run simultaneously. However, this is not always the reality when map-
ping streams to physical hardware. This section will illustrate how concurrent kernel operations in
multiple CUDA streams are scheduled by hardware.