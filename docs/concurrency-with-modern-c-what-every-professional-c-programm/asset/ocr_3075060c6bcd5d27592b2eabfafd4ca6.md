![](bbox=[0.146, 0.11, 0.856, 0.45])

Erroneous Busy Waiting with Resource Hierarchy (with optimization)

It is always the same philosopher thread that eats. Is it possible that the setting of compiler optimization can change the behavior of a program? Yes, it is possible. The philosopher threads read from memory the value of fork resource. The compiler optimization optimizes some of these memory reads away. Everything has a price!

# 6.2.5 Still Erroneous Busy Waiting with Resource Hierarchy

The programming language C++ has the atomic template to define an atomic type. If one thread writes to an atomic object while another thread reads from it, the behavior is well-defined. In file `dp_5.cpp` we use `atomic<int>` for the fork resources (lines 11, 17, 21, and 47). We include the header `<atomic>` in line 5.

Erroneous Busy Waiting with Resource Hierarchy

```
~~~cpp
// dp_5.cpp
#include <iostream>
#include <thread>
#include <chrono>
#include <atomic>

int myrand(int min, int max) {
    return rand()%(max-min)+min;
}

~~~
```