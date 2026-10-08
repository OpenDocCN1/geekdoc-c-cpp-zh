Like the host assert, evaluation of assert can be disabled for release versions of code by compiling with the NDEBUG pre-processor macro defined before assert.h is included.

# # Kernel Debugging Summary

This section focused on kernel debugging tools in CUDA, cuda-gdb, printf, and assert are all powerful tools that enable fine-grained debugging and error-checking of running CUDA kernels. Each has its own advantages and disadvantages.

cuda-gdb is the most powerful, allowing you to control kernel execution on the GPU, as well as interactive inspection of thread state across the entire kernel. As a result, cuda-gdb requires the most effort and also has a large impact on the performance of an application.

Even though printf is not interactive, it allows you to selectively print debugging messages from CUDA threads to quickly identify bugs in your code.

An assert is great for inspecting state when known issues or regressions arise while debugging, particularly when used with cuda-gdb. However, it is difficult to use effectively if you are debugging a new and unknown problem.

The next section focuses from directly debugging kernels to using kernel memory access errors to help pinpoint problems.

# # Memory Debugging

While cuda-gdb is useful for performing fine-grained inspection of CUDA kernel execution, and printf/assert are simple mechanisms for manual error checking, the primary tool used for debugging CUDA memory errors is cuda-memcheck. The operation of cuda-memcheck is more automated and coarse-grained in terms of user interaction, cuda-memcheck includes two separate units:

+   - The memcheck tool

+   - The racecheck tool

You use memcheck to check for out-of-bounds and misaligned accesses in CUDA kernels. racecheck can be used to detect conflicting accesses to shared memory, which could result in undefined behavior. These tools can be useful for erratic kernel behavior caused by threads reading and writing unexpected locations.

# # Compiling for cuda-memcheck

Compiling applications for cuda-memcheck is more complicated than cuda-gdb. When you build your application with -g -G, these options negatively affect performance. When using the cuda-memcheck tools, it is important that your application's performance remain consistent to ensure errors are reproducible. However, some compilation flags are necessary to help you dissect cuda-memcheck messages and pinpoint the problems occurs.