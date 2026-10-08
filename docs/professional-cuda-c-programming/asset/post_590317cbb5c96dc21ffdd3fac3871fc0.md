
application knows that each of those errors is distinct and different from the others (though cause can be related).

cudaPeekLastError performs the same checks as cudaGetLastError, but does not clear the internal state to be cudaSuccess.

cudaGetErrorString returns a human-readable string for the CUDA error passed to the function. This is useful for generating user-facing messages.

You will note that every downloadable example for the website makes use of error handling of some type or another, by using a CHECK or CALL_CUDA macro to exit on:

```c
#define CHECK(call) ( \
cuda_error_t err; \
if (err = (call)) != cudaSuccess) { \
fprintf(stderr, "Got error at %s:%d\n", cudaGetErrorString(err), \
FILE__, __LINE__); \
exit(1); //\
} )
```

In many applications it is possible to recover from CUDA errors, in which case an immediate exit is unnecessary.

# PROFILE-DRIVEN OPTIMIZATION

You must be very familiar with the profile-driven approach by now, as you have used this method to optimize kernel functions in every example throughout the book. There are two types of profile tools available for CUDA programming:

- NVIDIA profiling tools
- Third-party profiling tools

Most developers choose to use NVIDIA profiling tools because they are not only free, but also very powerful. Third-party profiling tools leverage NVIDIA profiling tool interfaces. Both graphical and command-line profiling tools are included in the CUDA toolkit.

Profile-driven optimization is an iterative process to optimize your program based on profile information. Typically, you use the following iterative approach:

1. Apply profile to an application to gather information.
2. Identify application hotspots.
3. Determine performance inhibitors.
4. Optimize the code.
5. Repeat the previous steps until desired performance is achieved.

The key step is to identify performance inhibitors. CUDA profiling tools will help you to locate inhibitors in your code. The most likely performance inhibitors for a kernel are:

- Memory bandwidth
- Instruction throughput
- Latency

In previous chapters, we used NVIDIA profiling tools to identify these inhibitors. This section briefly summarizes profile-driven optimization using both the Visual Profiler and Command-line Profiler.

# Finding Optimization Opportunities Using nvprof

The primary profiling tool for CUDA applications is nvprof. Roughly speaking, there are two types of profiling data you can collect using nvprof:

- A Timeline of CUDA-related activities on both the CPU and GPU
- Events and metrics for kernels

# Profiling Modes

nvprof is called from the command line with the following syntax:

```
nvprof [nvprof-options] <application> [application-arguments]
```

You can run nvprof in one of four modes:

- Summary mode
- Trace mode
- Event/Metric summary mode
- Event/Metric trace mode

By default, nvprof runs in Summary mode. You can use nvprof-options to switch to other modes. For example, Trace-trace can be enabled using the following options:

```
--print-gpu-trace
--print-api-trace
```

GPU-trace and API-trace modes can be enabled individually or at the same time. GPU-trace mode provides a timeline of all activities taking place on the GPU in chronological order. API-trace mode shows a timeline of all CUDA runtime and driver API calls invoked on the host.

You can enable event/metric summary mode using the following options:

```
--events <event names>
--metrics <metrics names>
```

The event/metric summary mode collects statistics about different events/metrics that occur in applications. Metrics are hardware counters observed during the execution of an application. Metrics are calculated based on events. For example, number of memory accesses and number of L1 cache hits are events supported by nvprof. Using these, a metric of how well the application can be derived. While there are built-in metrics, you can define your own metrics based on hardware counters gathered from the profiler. Using the following options, you can query all-built events and metrics supported by nvprof:

```
--query-events
--query-metrics
```

You can enable event/metric trace mode using the following option:

```
--aggregate-mode off [events|metrics]
trace mode, event and metric values are shown for each kernel execution. By default, event and metric values are aggregated across all SMs in the GPU.
```

# Profil Scope

By default, nvprof profiles all kernels launched on all CUDA devices. This profiling scope can be limited by the following option:

```
--devices <device IDs>
```

This option applies to the following modes/options:

```
--events
--metrics
--query-events
--query-metrics
```

When combined with the previous modes/options, the --devices option limits collection of events/metrics to the devices specified by <device IDs>.

# Memory Bandwidth

A kernel can operate on a variety of storage types, including:

- Shared Memory
- L1/L2 Cache
- Texture Cache
- Device Memory
- System Memory (via PCIe)

There are many events/metrics related to memory operations collectable from nvprof. With these events/metrics, you can evaluate the efficiency of a kernel operating on different types of memory. The following subsections summarize which events/metrics you should collect in typical cases.

# Global Memory Access Pattern

Optimally, global memory accesses should be aligned and coalesced. Any access pattern other than aligned and coalesced will result in replay of memory requests. You can use the following metrics to check the efficiency of global memory load and store operations in a kernel:

- gld_efficiency
- gst_efficiency

The metric gld_efficiency is defined as the ratio of the requested global memory load throughput to the required global memory load throughput does not include memory replay operations, while the required global memory load throughput does. The metric gst_efficiency is the same as gld_efficiency, but for global memory stores.

You can also use the following metrics to check global memory load and store efficiency:

- gld_transactions_per_request
- gst_transactions_per_request

The metric gld_transactions_per_request is the average number of global memory load transactions performed for each global load request. The metric gst_transactions_per_request is the average number of global memory store transactions performed for each global memory store request. If many transactions are required for a single global load or store, device memory bandwidth is being wasted.

You can check the total number of memory operations using the following metrics:

- gld_transactions
- gst_transactions

The metric gld_transactions is the number of global memory load transactions per kernel launch, and the metric gst_transactions is the number of global memory store transactions per kernel launch.

You can check the throughput of memory operations using the following metrics:

- gld_throughput
- gst_throughput

The metric gst_throughput is the global memory store throughput, and the metric gld_throughput is the global memory load throughput. You can compare these measured values with theoretical peak values to determine if your kernel is close to ideal performance, or if there is still room for improvement.

# Shared Memory Bank Conflicts

Bank conflicts are a major performance concern when using shared memory. You can use the following metrics to check if bank conflicts occur in your application:

- shared_load_transactions_per_request
- shared_store_transactions_per_request

Bank conflicts cause memory replays, and the corresponding value for either loads or stores will be greater than one.

You can also check directly for bank conflicts using the event:

```
l1_shared_bank_conflict
```

This event reports the number of shared bank conflicts due to two or more shared memory requests accessing the same bank.

Using the following event to collect the number of instructions executed for shared memory loads/stores, not including replays:

```
shared_load
shared_store
```

Then, you can calculate the number of replays per instruction as follows:

```
l1_shared_bank_conflict/(shared_load + shared_store)
```

You can also check shared memory efficiency using the metric:

```
shared_efficiency
```

The shared_efficiency metric is defined as the ratio of requested shared memory throughput to the required shared memory throughput. Because the required shared memory throughput includes replay, a lower ratio for shared_efficiency implies more bank conflicts.

# Register Spilling

When a kernel uses more register variables than the maximum allowed per thread (63 for Fermi and 255 for Kepler), the compiler will spill the values to local memory. Spilling to local memory can drastically degrade kernel performance. To evaluate the severity of register spilling, first collect the following events:

Then, calculate the ratios:

```
local_load_hit_ratio = l1_local_load_hit / (l1_local_load_hit + l1_local_load_miss)
local_store_hit_ratio = l1_local_store_hit / (l1_local_store_hit + l1_local_store_miss)
```

A low ratio is indicative of severe register spilling. You can also check the following metric:

```
l1_cache_local_hit_rate
```

This metric reports the hit rate in L1 cache for local loads and stores. If more local loads and stores are being performed, it means more spilling may have occurred.
