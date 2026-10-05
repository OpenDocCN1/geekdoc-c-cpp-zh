for special applications like cameras, cars, or networked LEDs (so-called embedded systems) might be somewhat more restricted.

Compute threads burden the CPU resource. Allowing more than one thread to compute on a CPU would be wasteful and unnecessary. But first, compute threads also need to wait from time to time and can yield their capacities to another thread during that time, and second, it is not really bad to have slightly more threads than CPUs. However, having significantly more threads than CPUs is not good because it leads to more thread switches additional resources on top of what a thread itself costs. The rule of thumb is that you can run one to two times as many compute threads in parallel as you have CPU cores without overloading the system.

So if you want to know the optimal number of threads for a computational program, you first need to find out how many CPUs your machine has. This number times one or two is then the maximum number of computational threads I recommend. For this purpose, there is the following:

```
std::thread::hardware_concurrency()
```

This function provides a hint about the number of threads that can actually run in parallel on the system. However, the function can also return 0 if the information is not available.