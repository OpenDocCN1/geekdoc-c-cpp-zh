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

# Profiling Scope

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

+   * Shared Memory
* L1/L2 Cache
* Texture Cache
* Device Memory
* System Memory (via PCIe)

There are many events/metrics related to memory operations collectable from nvprof. With these events/metrics, you can evaluate the efficiency of a kernel operating on different types of memory. The following subsections summarize which events/metrics you should collect in typical cases.