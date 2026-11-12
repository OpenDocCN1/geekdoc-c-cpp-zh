some time to provide the GPU with additional work. In the example we have here, the CPU is simply checking the array against a set of expected values, but it could be doing a much slower operation such as loading the next work unit from disk. In this case we'd like the GPU to remain busy during this period also. For this we use a scheme called double buffering.

Double buffering works by having the GPU work with one buffer while the CPU is working with the other buffer. Thus, even while the CPU is processing one dataset, the GPU is still performing useful work, rather than waiting on the CPU. The CPU process may be something as simple as loading or saving data to disk. It might also include some additional processing and/or combination of data from multiple GPUs.

To do this we need to introduce another dimension to every array based on MAX_NUM_DEVICES. For example:

```
// Define N streams per GPU
cudaStream_t stream[MAX_NUM_DEVICES][MAX_NUM_STREAMS];
```

Then we have the option to support two or more streams per device. Using two streams per device has a small problem, in that if we allocate work units to GPUs with equal priority, they all get the same total number of work units. This, in practice, means we end up at the end of the work queue, still waiting on the slowest device. The solution to this is to allocate work units to the GPUs in proportion to their speed.

If you look back at Figure 8.3, you can see that the GT9800 is the slowest device. The GTX260 is approximately twice as fast, the GTX460 twice as fast again, and the GTX470 around 20% faster than the GTX460. Given that we want at least two streams to allow for double buffering, if we increase the number of streams allocated in proportion to the speed of the device, we get a work distribution that keeps all devices busy for about the same amount of time. We can do this with a simply array:

```
// Define the number of active streams per device
const u32 streams_per_device[MAX_NUM_DEVICES] =
[
10, /* GTX470 */
2, /* 9800 GTX */
4, /* GTX260 */
8, /* 460 GTX */
];
```

Thus, initially we allocate 10 work units to device 0, the GTX470. However, we allocate only 2 work units to the GT9800, and so on. At the point we run out of work units each device has the queue length of approximately the value shown in the array. As this equates to approximately the same time, all devices finish within a short period of one another.

Here the list of the relative speeds of the various GPUs is constructed statically. If you always have the same hardware in the target machine, then this approach is fine. However, if you don't know what the target hardware is, you can do some initial timing runs and then complete such a table at runtime. The important point to remember is the minimum value in the list should always be at least 2 to achieve double buffering. The other values should be some multiple of 2, which reflects the relative timing to the slowest device.