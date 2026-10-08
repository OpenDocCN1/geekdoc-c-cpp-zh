> > Compute Capability 3.5 hardware with 15 multi-processors
> CUDA_DEVICE_MAX_CONNECTIONS = 8
> with streams = 4
 callback from stream 0
 callback from stream 1
 callback from stream 2
 callback from stream 3
 Measured time for parallel execution = 0.104s

# # SUMMARY

The concept of streams is a fundamental part of the CUDA programming model. CUDA streams allow coarse-grained concurrency by permitting high-level CUDA operations to be queued to independent streams. Because CUDA supports an asynchronous, version of most runtime functions, it is possible to distribute computation and communication among multiple CUDA streams.

Conceptually, if there are dependencies between CUDA operations they must be scheduled in the same stream. For example, to ensure correctness a kernel must be scheduled in the same stream and after any data it consumes. Otherwise, operations with no dependencies can be scheduled in arbitrary times. In CUDA, you can typically use three different types of overlap schemes to hide computation or communication latencies:

+   - Overlap of multiple, concurrent kernels on the device
- Overlap of CUDA kernels with data transfer to or from the device
- Overlap of CPU execution and GPU execution

To fully utilize the device and ensure maximum concurrency, you also need to be mindful of the following issues:

+   - Balance kernel resource requirements and concurrency resource requirements. Launching many computational tasks on the device may result in kernel serialization when resources available. However, you also need to ensure that the device is not underutilized and that there is always queued up for execution.
- Avoid using the default stream to execute asynchronous operations if possible. Operations placed in the default stream might block progress of other non-default CUDA streams.
- On a Fermi device, consider both depth-first and breadth-first dispatch from the host. This can significantly impact performance by eliminating false dependencies in the shared hardware queue.
- Be mindful of implicit synchronization functions, and use them carefully with asynchronous functions to avoid degraded performance.

In addition, this chapter demonstrated the usefulness of the CUDA Visual Profiler (nvvp) in visualizing GPU execution. nvvp allows you to identify opportunities for operation overlap, and makes it easy to visualize the behavior of multiple streams.