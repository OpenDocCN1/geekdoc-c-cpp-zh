# Atomic Operations

Atomic operations are indivisible operations supported directly by the hardware. CUDA provides a variety of atomic operations such as and atomicCAS (compare and swap), among others. These operations are essential tools for implementing synchronization mechanisms, including locks and counters, without the explicit use of barriers or mutexes.

Example of using atomicAdd to safely increment a global counter:

```
__global__ void *counter) { 1); }
```