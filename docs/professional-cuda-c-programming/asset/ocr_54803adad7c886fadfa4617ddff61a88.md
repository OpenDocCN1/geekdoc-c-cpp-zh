application knows that each of those errors is distinct and different from the others (though cause can be related).

cudaPeekLastError performs the same checks as cudaGetLastError, but does not clear the internal state to be cudaSuccess.

cudaGetErrorString returns a human-readable string for the CUDA error passed to the function. This is useful for generating user-facing messages.

You will note that every downloadable example for the website makes use of error handling of some type or another, by using a CHECK or CALL_CUDA macro to exit on:

```
#define CHECK(call) ( \
cuda_error_t err; \\
if (err = (call)) != cudaSuccess) { \\
fprintf(stderr, "Got error at %s:%d\n", cudaGetErrorString(err), \\
FILE__, __LINE__); \\
exit(1); //\
} )
```

In many applications it is possible to recover from CUDA errors, in which case an immediate exit is unnecessary.

# PROFILE-DRIVEN OPTIMIZATION

You must be very familiar with the profile-driven approach by now, as you have used this method to optimize kernel functions in every example throughout the book. There are two types of profile tools available for CUDA programming:

+   - NVIDIA profiling tools
- Third-party profiling tools

Most developers choose to use NVIDIA profiling tools because they are not only free, but also very powerful. Third-party profiling tools leverage NVIDIA profiling tool interfaces. Both graphical and command-line profiling tools are included in the CUDA toolkit.

Profile-driven optimization is an iterative process to optimize your program based on profile information. Typically, you use the following iterative approach:

+   1. Apply profile to an application to gather information.
2. Identify application hotspots.
3. Determine performance inhibitors.
4. Optimize the code.
5. Repeat the previous steps until desired performance is achieved.