# NVIDIA Tools Extension

NVIDIA provides a utility that allows developers to annotate events, code ranges, and resources in an application. The Visual Profiler can then be used to capture and visualize these events and code ranges. This extension, NVTX, is a C-based API with two code services:

+   - Tracing CPU events and code ranges
- Naming of OS and CUDA resources

This section demonstrates how to integrate NVTX into an application using the matrix sum example. You can download the example using sumMatrixGPU.cu from Wrox.com. Compile and run it with nvvp as follows:

```
$ nvcc -o sumMatrix sumMatrixGPU.cu
$ nvvp ./summatrix
```

Figure 10-8 illustrates the timeline of this sum program. Only events related to GPU computation or communication were recorded in this timeline. To display code events in the timeline, you can use the NVTX API to highlight the relevant code ranges so nvvp can generate the timeline for events.

![](bbox=[0.066, 0.455, 0.866, 0.638])

FIGURE 10-8

Starting with sumMatrixGPU.cu, include the following header files:

```
#include <nvToolsExt.h>
#include <nvToolsCuda.h>
#include <nvToolsExtCudaRt.h>
```

The core NVTX API functions are defined in nvToolsExt.h. CUDA-specific extensions to the NVTX interface are defined in nvToolsExtCuda.h and nvToolsExtCudaRt.h.