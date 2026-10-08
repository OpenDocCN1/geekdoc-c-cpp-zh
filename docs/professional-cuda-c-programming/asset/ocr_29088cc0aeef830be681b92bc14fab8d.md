nvvp is a Visual Profiler, which helps you to visualize and optimize the performance of your CUDA program. This tool displays a timeline of program activity on both the CPU and GPU, helping you identify opportunities for performance improvement. In addition, nvvp analyzes your application for potential performance bottlenecks and suggests actions to eliminate or reduce them. The tool is available as both a standalone application and part of the Nsight Eclipse Edition (nsight).

nvprof collects profiling data on the command line. nvprof was introduced with CUDA 5 and replaces an older command-line CUDA profiling tool. Like nvvp, it enables the collection of a timeline of CUDA-related activities on both the CPU and GPU, including kernel execution, memory transfers, and CUDA API calls. It also enables you to collect hardware counters and performance metrics for CUDA kernels.

In addition to predefined metrics, you can also define your own metrics based on hardware counters gathered by the profiler.

EVENTS AND METRICS

In CUDA profiling, an event is a countable activity that corresponds to a hardware counter collected during kernel execution. A metric is a characteristic of a kernel calculated from one or more events. Keep in mind the following concepts about events and metrics:

 Most counters are reported per streaming multiprocessor but not the entire GPU.
* A single run can only collect a few counters. The collection of those counters is mutually exclusive. Multiple profiling runs are often needed to gather all relevant counters.
* Counter values may not be the same across repeated runs due to variations in GPU execution (such as thread block and warp scheduling).

To identify the performance bottleneck of a kernel, it is important to choose appropriate performance metrics and compare measured performance to theoretical peak performance. Throughout the examples and exercises in this book, you will learn about the proper metrics for analyzing kernels with the command-line profiler and master the skill of writing an efficient kernel using the profile-driven approach.

In this book, you will mainly use nvprof to dissect your kernel with the goal of improving performance. You will learn how to select appropriate counters and metrics, and use nvprof to collect profiling data, which can then be used in an optimization strategy. You will learn how to analyze your kernel from multiple angles using different counters and metrics.