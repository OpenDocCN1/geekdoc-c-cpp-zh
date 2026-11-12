This API follows stream ordering semantics, i.e. the migration does not begin until all prior operations in the stream have completed, and any subsequent operation in the stream does not begin until the migration has completed.

# K.3.2. Data Usage Hints

Data prefetching alone is insufficient when multiple processors need to simultaneously access the same data. In such scenarios, it's useful for the application to provide hints on how the data will actually be used. The following advisory API can be used to specify data usage:

```
cudaError_t cudaMemAdvise(const void *devPtr,
 size_t count,
 enum cudaMemoryAdvise advice,
 int device);
```

where **advice**, specified for data contained in region starting from **devPtr** address and with the length of **count** bytes, rounded to the nearest page boundary, can take the following values:

+   **cudaMemAdviseSetReadMostly:** This implies that the data is mostly going to be read from and only occasionally written to. This allows the driver to create read-only copies of the data in a processor's memory when that processor accesses it. Similarly, if **cudaMemPrefetchAsync** is called on this region, it will create a read-only copy of the data on the destination processor. When a processor writes to this data, all copies of the corresponding page are invalidated except for the one where the write occurred. The **device** argument is ignored for this advice. This advice allows multiple processors to simultaneously access the same data at maximal bandwidth as illustrated in the following code snippet:

```
char *dataPtr;
size_t dataSize = 4096;
// Allocate memory using malloc or cudaMallocManaged
data = (char *)malloc(dataSize);
// Set advice on the memory region
cudaMemAdvise(dataPtr, dataSize, cudaMemAdviseSetReadMostly, 0);
int outerLoopIter = 0;
while (outerLoopIter < maxOuterLoopIter) {
 // The data is written to in the outer loop on the CPU
 initializeData(dataPtr, dataSize);
 // Prefetching here makes available to all GPUs by prefetching.
 // Prefetch here causes read duplication of data instead
 // of data migration
 for (int device = 0; device < maxDevices; device++) {
 cudaMemPrefetchAsync(dataPtr, dataSize, device, stream);
 }
 // The kernel only reads this data in the inner loop
 int innerLoopIter = 0;
 while (innerLoopIter < maxInnerLoopIter) {
 kernel<<<32, 32>>>((const char *)dataPtr);
 innerLoopIter++;
 }
 outerLoopIter++;
}
```

+   **cudaMemAdviseSetPreferredLocation:** This advice sets the preferred location for the data to be the memory belonging to **device**. Passing in a value of **cudaCpuDeviceId** for **device** sets the preferred location as CPU memory. Setting the preferred location does not cause data to migrate to that location immediately.