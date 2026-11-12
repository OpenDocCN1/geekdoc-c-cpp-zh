embeds binary code compatible with compute capability 3.5 and 5.0 (first and second -gencode options) and PTX and binary code compatible with compute capability 6.0 (third -gencode option).

Host code is generated to automatically select at runtime the most appropriate code to load and execute, which, in the above example, will be:

+   - 3.5 binary code for devices with compute capability 3.5 and 3.7,
+   - 5.0 binary code for devices with compute capability 5.0 and 5.2,
+   - 6.0 binary code for devices with compute capability 6.0 and 6.1,
+   - PTX binary code which is compiled to binary code at runtime for devices with compute capability 7.0 and higher.

x. cu can have an optimized code path that uses warp shuffle operations, for example, which are only supported in devices of compute capability 3.0 and higher. The __CUDA_ARCH__ macro can be used to differentiate various code paths based on compute capability. It is only defined for device code. When compiling with -arch=compute_35 for example, __CUDA_ARCH__ is equal to 350.

Applications using the driver API must compile code to separate files and explicitly load and execute the most appropriate file at runtime.

The Volta architecture introduces Independent Thread Scheduling which changes the way threads are scheduled on the GPU. For code relying on specific behavior of SIMT scheduling in previous architectures, Independent Thread Scheduling may alter the set of participating threads, leading to incorrect results. To aid migration while implementing the corrective actions detailed in Independent Thread Scheduling, Volta developers can opt-in to Pascal's thread scheduling with the compiler option combination -arch=compute_60 -code=sm_70.

The nvcc user manual lists various shorthands for the -arch, -code, and -gencode compiler options. For example, -arch=sm_35 is a shorthand for -arch=compute_35 -code=compute_35,sm_35 (which is the same as -gencode arch=compute_35,code='compute_35,sm_35').

# ## 3.1.5. C++ Compatibility

The front end of the compiler processes CUDA source files according to C++ syntax rules. Full C++ is supported for the host code. However, only a subset of C++ is fully supported for the device code as described in C++ Language Support.

# ## 3.1.6. 64-Bit Compatibility

The 64-bit version of nvcc compiles device code in 64-bit mode (i.e., pointers are 64-bit). Device code compiled in 64-bit mode is only supported with host code compiled in 64-bit mode.

Similarly, the 32-bit version of nvcc compiles device code in 32-bit mode and device code compiled in 32-bit mode is only supported with host code compiled in 32-bit mode.

The 32-bit version of nvcc can compile device code in 64-bit mode also using the -m64 compiler option.