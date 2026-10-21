```
for (int i=0; i<numElems; ++i) {
    coll.push_back(Data{i * 4.37, 0});
}

// parallel computation of square roots:
for_each(std::execution::par,
        coll.begin(), coll.end(),
        [](auto& val) {
            val.sqrt = std::sqrt(val.value);
        });
```

As you can see, using the parallel algorithms is in principle pretty easy:

+   - Include header <execution>
+   - Call the algorithms the way you would usually call algorithms with an additional first argument, which will often simply be std::execution::par.

In this case, we use the standard algorithm for_each() to compute the square root of the members value of all elements in the passed vector coll. Due to the additional first parameter std::execution::par, we request that the algorithm runs in parallel mode:

```
#include <algorithm>
#include <execution>
...
for_each(std::execution::par,
        coll.begin(), coll.end(),
        [](auto& val) {
            val.sqrt = std::sqrt(val.value);
        });
```

As usual, coll might be any range here. However, note that all parallel algorithms require the iterators to be at least forward iterators (we iterate through the same elements in different threads, which makes no sense if the iterators would not iterate over the same values).

The way the algorithms run in parallel is implementation-specific. And of course, using multiple threads might not always be faster, because starting and dealing with multiple threads also takes time.

# Performance Benefits

To find out how to run and whether, and when it is worth running this algorithm in parallel, let us modify the example as follows:

lib/parforeachloop.cpp

```
#include <vector>
#include <iostream>
#include <algorithm>
#include <numeric>
#include <execution>  //for the execution policy
```