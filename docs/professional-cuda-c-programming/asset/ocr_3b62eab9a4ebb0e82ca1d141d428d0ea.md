the functionality is __dsqrt_rn. There is an intrinsic function for single-precision floating-point division, __fdivf.

Intrinsic functions decode fewer instructions than their equivalent standard functions. As a result, intrinsic functions are faster than their equivalent standard functions but less numerically precise. This gives you the capability to use standard and intrinsic functions interchangeably, but produce different program behavior in both performance and numerical accuracy.

Standard and intrinsic functions add a significant amount of flexibility to CUDA application. They serve as fine-grained knots that you can turn to tweak performance and numerical accuracy on an operation-by-operation basis. In a later section of this chapter titled, "Standard vs. Intrinsic Functions" you will get hands-on experience adjusting these to explore their effects.

# # Atomic Instructions

An atomic instruction performs a mathematical operation, but does so in a single uninterrupted operation without interference from other threads. When a thread successfully completes an atomic operation on a variable, it can be certain that the variable's state has changed no matter how many other threads are accessing that variable. Atomic instructions prevent multiple threads from interfering with each other, and enable read-modify-write operations for shared data (for example, read the current value, increment it, and write the new value). Guaranteeing the atomicity of read-modify-write operations is especially important in highly concurrent environments. The GPU provides atomic functions that perform read-modify-write atomic operations on 32-bits or 64-bits of global memory or shared memory.

While any device compute 1.1 or higher support atomic operations, Kepler-based global memory operations are faster than Fermi-based operations, leading to dramatically higher throughput. This may enable CUDA-based applications that were previously deemed impractical for GPU execution because of their heavy reliance on atomic operations.

Like standard and intrinsic functions, each atomic function implements a basic operation such as addition, multiplication, or subtraction. Unlike any other instruction type described so far, atomic instructions have a defined behavior when operating on a memory location shared by two competing threads.

Consider the following kernel to help you understand this:

```
global void incr(int *ptr) {
    int temp = *ptr;
    temp = temp + 1;
    *ptr = temp;
}
```

This kernel reads from a memory location, adds one to the value, and then writes the calculated value back to the same location. Note that no IDs are used to change the memory locations being accessed; every thread in a kernel launch will read and write from the same address. If a single block of 32 threads were launched running this kernel, what output would you expect? You might say 32: Each thread will increment by one. In truth, the result is undefined. The problem here is that more than one thread writing to the same memory location. This is called a data race, or unsafe access to memory. A data race is defined as two or more independent