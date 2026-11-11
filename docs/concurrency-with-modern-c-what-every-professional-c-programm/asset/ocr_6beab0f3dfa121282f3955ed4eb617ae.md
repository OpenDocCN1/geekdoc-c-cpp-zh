![](bbox=[0.26, 0.115, 0.74, 0.262])

![](bbox=[0.26, 0.3, 0.74, 0.45])

and Windows.

# 12.6.3 Single-Threaded Summation with Synchronization (atomic)

The following range-based for-loop uses and atomic for synchronization. Here are the essential lines showing the difference to the non-synchronized version.

Summation of a vector by using an atomic for the summation variable

```
~~~cpp
// calculateWithAtomic.cpp

...

std::atomic<unsigned long long> sum = {};

for (auto i : randValues) sum += i;

...
~~~
```

Respectively, the performance numbers for Linux