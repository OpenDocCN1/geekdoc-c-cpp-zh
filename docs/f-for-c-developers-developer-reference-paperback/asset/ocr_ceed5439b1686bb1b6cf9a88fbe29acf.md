# FIGURE 9-4 Getting the device limitations execution result

For device management, there are other commonly used functions (which are shown in\ Listing 9-5):

+   - **Reset function** This function cleans up all resources on the current device associated with the current process. If there are multiple threads on the current process, it is the developer's responsibility to make sure the other thread or threads do not access this device.
- **Get device count function** This function returns the number of devices.\n- **Set device flag function** This is useful for allowing you to set flags to configure how the GPU and CPU work together.

When the GPU is processing the data, there is a CPU thread waiting for the result to come back. The following flags configure how the CPU thread waits for the return value:

+   - `cudaDeviceScheduleAuto` is used as a default value. If the active CUDA context number is larger than the logical processor, the thread can yield to other operating systems threads. Otherwise, the CUDA will spin on the CPU processor and not yield to other processors.
- `cudaDeviceScheduleSpin` instructs the CUDA thread on the CPU to never yield to other threads until it gets the result from the device. This can increase the CPU latency, but it can decrease the latency waiting for results from the device.
- `cudaDeviceScheduleSpin` is the opposite of `cudaDeviceScheduleSpin`. It instructs the CUDA thread to yield to other operating systems threads on the CPU when waiting for the threads.
- `cudaDeviceScheduleBlockingSync` instructs a CUDA thread on the CPU to block other CPU threads when waiting for the result of the device.

# LISTING 9-5 Device flag definition

```
Code definition
type cudaDeviceFlag =
| cudaDeviceScheduleAuto = 0
| cudaDeviceScheduleSpin = 1
| cudaDeviceScheduleYield = 2
| cudaDeviceScheduleBlockingSync = 4

[DllImport(dllName)]
extern cudaDeviceReset()

[DllImport(dllName)]
extern cudaError cudaGetDeviceCount(int&count)
```