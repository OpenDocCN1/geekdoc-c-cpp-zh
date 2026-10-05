# Characteristics of Global Memory

Global memory is off-chip and, as such, exhibits higher access times. Despite these challenges, it’s essential for handling large-scale problems that exceed the capacity of shared and local memory. It’s important to note that:

Accesses to global memory are not Every read or write request traverses the memory bus, contributing to higher latency.
The bandwidth of global memory, although significantly lower than shared or local memory, is still substantial, making it possible to achieve high throughput under certain access patterns.
Global memory can be dynamically allocated and deallocated at runtime, providing flexibility in managing memory resources for complex applications.