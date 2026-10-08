![](bbox=[0.095, 0.096, 0.866, 0.313])

FIGURE 6-13

# # Creating Inter-Stream Dependencies

Ideally, there would be no unintended dependencies between streams (that is, false dependencies). However, in complex applications it can be used to introduce inter-stream dependencies that block operations in one stream until operations in another stream have completed. Events can be used to add inter-stream dependencies.

Suppose you want the work in one stream to only start after all other streams complete. You can use events to create a dependency between streams. First, create synchronization-only events with the flag cudaEventDisableTiming, as:

```
cudaEvent_t *kernelEvent = (cudaEvent_t*)malloc(n_streams * sizeof(cudaEvent_t));
for (int i = 0; i < n_streams; i++) {
    cudaEventCreateFlags(&kernelEvent[i], cudaEventDisableTiming);
}
```

Next, create an event to track the completion of each stream using cudaRecord. Then, use cudaStreamWait to force the last stream (that is, streams [n_streams-1]) to wait for all other streams:

```
// dispatch job with depth first
for (int i = 0; i<n_streams; i++) {
    kernel_1<<<grid, block, 0, streams[i]>>>();
    kernel_2<<<grid, block, 0, streams[i]>>>();
    kernel_3<<<grid, block, 0, streams[i]>>>();
    kernel_4<<<grid, block, 0, streams[i]>>>();
}
ncudaEventRecord(kernelEvent[i], streams[i]);
cudaStreamWait(streams[n_streams-1], kernelEvent[i], 0);
```

You can download the full code for this example in the file simpleHyper.cu from Wrox.com. Figure 6-14 shows the nvvp timeline. Note that the fourth stream, streams [n_streams-1], only starts its work after all other streams complete.