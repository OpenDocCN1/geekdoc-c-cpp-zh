![](bbox=[0.227, 0.105, 0.78, 0.306])

simplifying CRTP

# ## 8.1.2 The Standard Library

# ### 8.1.2.1 Ranges Extensions

The ranges library got powerful extensions in C++23. This extension includes a convenient way to construct a container, various new views, and with `std::generator` the first concrete coroutine.

# #### 8.1.2.1.1 ranges::to

`std::ranges::to` is a convenient way to construct a container from a range:

```
~~~cpp
std::vector<int> range(int begin, int end, int stepsize = 1) {
    auto boundary = [end](int i){ return i < end; };
    std::vector<int> result = std::ranges::views::iota(begin)
                            | std::views::stride(stepsize)
                            | std::views::take_while(boundary)
                            | std::ranges::to<std::vector>();
    return result;
}
~~~
```

The function `range` creates a `std::vector<int>` consisting of all elements from `begin` to `end` with the `stepsize` stepsize. `begin` must be smaller than `end`. Thanks to `std::ranges::to`, the element can be directly pushed into the `std::vector`.

# #### 8.1.2.1.2 New Views

C++23 supports additional views: