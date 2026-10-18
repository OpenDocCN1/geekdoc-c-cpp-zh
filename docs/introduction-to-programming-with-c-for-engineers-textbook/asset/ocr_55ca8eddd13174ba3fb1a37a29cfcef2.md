where

$$m_x = \frac{1}{N}\sum_{i=1}^{N}x_i$$

denotes the mean value of a vector **x**, and **N** stands for the number of elements in the vector.

+   a. Implement a serial version of this two-pass algorithm.³
+   
+   b. Write a test function that will (i) create a vector with randomly generated values from a given distribution and (ii) compute their variance.
+   
+   c. Implement a parallel version of the two-pass algorithm. Compare the return values and execution times of the serial and parallel versions.
+   
+   d. Apply the compensated summation algorithms discussed in Section 7.4.7. Compare the results.

+   7. C++20 comes with an interesting feature – *coroutines*. These are functions that can suspend execution and store the current state, to be resumed later with the state restored. This allows for a number of interesting mechanisms such as *asynchronous tasks*, non-blocking I/O handling, value generators, etc. A function becomes a coroutine if it contains any of the following constructions: `co_await`, `co_yield`, or `co_return`. For example, the following `next_int_gen` coroutine returns the consecutive integer value on each call:

```
```cpp
generator<int> next_int_gen(int val = 0)
{
    for(;;)
        co_yield val++;
}
```
```

`co_yield` suspends execution of the `next_int_gen` function, stores the state of `val` object in the `generator<int>`, and returns the current value of `val` through the `generator<int>` object.

+   a. Read more about coroutines (https://en.cppreference.com/w/cpp/language/coroutines), and write a test function to experiment with `next_int_gen`.
+   
+   b. Try to implement a new version of the range class from Section 6.5, using coroutines.

+   8. Implement a parallel version of the MSE defined in Table 8.3 using the `std::transform_reduce`. Compare performance of your implementation with the OpenMP based version.

+   9. Using the `std::transform_reduce` and the `std::filesystem::recursive_directory_iterator` implement a serial code to recursively traverse a given directory and to sum up sizes of all regular files (see Section 6.2.7). Then design a parallel solution. However, since the above iterator cannot be directly used in a parallel version of the `transform_reduce`, implement a producer-consumer scheme.