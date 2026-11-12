# # CHANGES FROM VERSION 10.0

+   - Use CUDA C++ instead of CUDA C to clarify that CUDA C++ is a C++ language extension not a C language.
+   - General wording improvements throughout the guide.
+   - Fixed minor typos in code examples.
+   - Updated From Graphics Processing to General Purpose Parallel Computing.
+   - Added reference to NVRTX in Just-in-Time Compilation.
+   - Clarified linear memory address space size in Device Memory.
+   - Clarified usage of CUDA_API_PER_THREAD_DEFAULT_STREAM when compiling with nvccin Default Stream.
+   - Updated Host Functions (Callbacks) to use cudaLaunchHostFunc instead of the deprecated cudaStreamAddCallback.
+   - Clarified that 8 GPU peer limit only applies to non-NVSwitch enabled systems in Peer-to-Peer Memory Access.
+   - Added section IOMMU on Linux.
+   - Added reference to CUDA Compatibility in Versioning and Compatibility.
+   - Extended list of types supported by __ldg() function in Read-Only Data Cache Load Function.
+   - Documented support for unsigned short int with atomicCAS().
+   - Added section Address Space Predicate Functions.
+   - Added removal notice for deprecated warp vote functions on devices with compute capability 7.x or higher in Warp Vote Functions.
+   - Added documentation for __nv_aligned_device_malloc() in Dynamic Global Memory Allocation and Operations.
+   - Added documentation of cudaLimitStackSize in CUDA Dynamic Parallelism Configuration Options.
+   - Added synchronization performance guideline to CUDA Dynamic Parallelism Synchronization.
+   - Documented performance improvement of roundf(), round() and updated Maximum ULP Error Table for Mathematical Standard Functions.
+   - Updated Performance Guidelines Multiprocessor Level for devices of compute capability 7.x.
+   - Clarified Shared Memory carve out description in Compute Capability 7.x Shared Memory.
+   - Added missing Stream CUstream Mapping to Driver API
+   - Added remark about driver and runtime API inter-operability, highlighting cuDevicePrimaryCtxRetain() in Driver API Context.
+   - Updated default value of CUDA_CACHE_MAXSIZE and removed no longer supported environment variables from CUDA Environment Variables
+   - Added new Unified Memory sections: System Allocator, Hardware Coherency, Access Counters
+   - Added section External Resource Interoperability .