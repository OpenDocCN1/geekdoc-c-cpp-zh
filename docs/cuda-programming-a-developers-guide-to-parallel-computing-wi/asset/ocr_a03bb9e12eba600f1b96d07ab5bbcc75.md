```
if ( cudaEventQuery( memcpy_to_stop[device_num][complete_count_in_stop[device_num]] )
    == cudaSuccess )
{
    TIMER_T delta = 0.0F;
    CUDA_CALL( cudaEventElapsedTime( &delta, memcpy_to_start[device_num][0],
        memcpy_to_stop[device_num][complete_count_in_stop[device_num]] ) );
    printf( "%sMemcpy to device test %d completed %.2f ms", device_prefix(device_num),
        complete_count_in_stop[device_num], delta );
    complete_count_in_stop[device_num]++;
    event_completed = true;
}
```

In this particular example, taken from another program, we have an array of events, memcpy_to_stop, indexed by device number and test number. We check if the event has completed by a call to cudaEventQuery(), which returns cudaSuccess if the event has already completed. If so, we get the delta time between this event and the start event memcpy_to_start from the same device, but for test 0, we get the start event for the whole kernel stream to that GPU. To obtain the delta time we simply call the cudaEventElapsedTime function.

Note that this will generate an error if the event has not yet completed, it is guarded by the check with cudaEventQuery(). We could equally call cudaEventSynchronize if we simply wanted a blocking call that would wait for the event to complete.

If we're particularly interested in the absolute time, the GPU does provide access to the low-level timers with the help of some embedded PTX code:

```
// Fetch the lower 32 bits of the clock (pre compute 2.x)
unsigned int clock;
asm("mov.u32 %0, %clock;" : "=r"(clock));

// Fetch the clock (compute 2.x)
unsigned long long int clock64;
asm("mov.u64 %0, %clock64;" : "=r"(clock64));
```

This section of code loads the raw clock value into a C variable that can then later be stored in a history buffer and transferred back to the host. The special %clock value is simply a 32-bit counter that wraps at max(u32). Compute 2.x hardware provides a 64-bit clock, thus allowing a wider time range over which values can be timed. Note, the CUDA API provides functions to access these register values through the use of the clock and clock64 functions.

You can use this to measure the times of device functions within kernel calls or sections of code. Such measurements are not shown with either the Visual Profiler or Parallel Nsight, as their resolution onto the timing stops at the global-level kernel functions. You can also use this to store the times warps arrive at a barrier point. Simply create a store on a per-warp basis prior to a call to a barrier primitive such as __syncthreads(). You can then see the distribution of the warps to the synchronization point.

However, one very important caveat here is you must understand that a given warp in a kernel will not be running all the time. Thus, as with timing multiple streams, a warp may store a start time, get