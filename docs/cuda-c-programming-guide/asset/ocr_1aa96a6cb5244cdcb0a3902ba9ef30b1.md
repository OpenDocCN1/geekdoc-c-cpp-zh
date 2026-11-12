those using the Virtual ISA (PTX). Part of this system defines the managed memory space that opts in to Unified Memory services.

Managed memory is interoperable and interchangeable with device-specific allocations, such as those created using the `cudaMalloc()` routine. All CUDA operations that are valid on device memory are also valid on managed memory; the primary difference is that the host portion of a program is able to reference and access the memory as well.

> Unified memory is not supported on discrete GPUs attached to Tegra.

# K.1.1. System Requirements

Unified Memory has two basic requirements:

+   - a GPU with SM architecture 3.0 or higher (Kepler class or newer)
+   - a 64-bit host application and non-embedded operating system (Linux, Windows, macOS)

GPUs with SM architecture 6.x or higher (Pascal class or newer) provide additional Unified Memory features such as on-demand page migration and GPU memory oversubscription that are outlined throughout this document. Note that currently these features are _only_ supported on Linux operating systems. Applications running on Windows (whether in TCC or WDDM mode) or macOS will use the basic Unified Memory model as on pre-6.x architectures even when they are running on hardware with compute capability 6.x or higher. See Data Migration and Coherency for details.

# K.1.2. Simplifying GPU Programming

Unification of memory spaces means that there is no longer any need for explicit memory transfers between host and device. Any allocation created in the managed memory space is automatically migrated to where it is needed.

A program allocates managed memory in one of two ways: via the `cudaMallocManaged()` routine, which is semantically similar to `cudaMalloc()`; or by defining a global `__managed__` variable, which is semantically similar to a `__device__` variable. Precise definitions of these are found later in this document.

> On supporting platforms with devices of compute capability 6.x and higher, Unified Memory will enable applications to allocate and share data using the default system allocator. This allows the GPU to access the entire system virtual memory without using a special allocator. See System Allocator for more detail.