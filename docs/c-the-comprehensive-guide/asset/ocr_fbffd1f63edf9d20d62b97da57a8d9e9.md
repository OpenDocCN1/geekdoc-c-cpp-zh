It should be noted that the end of the range always points to the element **after** the last element of the range. `data.begin()+4` refers to the `3` in `data`; therefore, deletion occurs from `5` up to **before** `3`. This applies to all methods of all standard containers and free functions with iterators, with the exception of some methods of `forward_list`.

This is also the reason that the `end()`s of all containers point **behind** the last element. Thus, they can be used easily in algorithms for range specification.

There are many algorithms. In the `<algorithm>` and `<numeric>` headers, you will find very, very many of them. For example, you can sort almost any standard container by calling (essentially) the following:

```
```cpp
#include <algorithm>
int main() {
    //...
    std::sort(begin(container), end(container));
    // or with ranges:
    std::ranges::sort(begin(container), end(container));
}
```
```

With `map` or `set` you don't need to try that, because they are already sorted. But `list`, `vector`, and `array` can be sorted this way.

Finally, you can extend iterators and equip them with new functionalities. For example, in the next listing, see how you can use an `ostream_iterator` output iterator to output the contents of any container to `cout`.

```
```cpp
// https://godbolt.org/z/7Xycqqh68
#include <vector>
#include <iostream>   // cout
#include <iterator>   // ostream_iterator
#include <algorithm>  // copy

int main() {
    std::vector data { 1, 2, 3, 7, 9, 10 };
    std::ostream_iterator<int> out_it (std::cout, ", "); // when assigned to cout
    std::copy(data.begin(), data.end(), out_it); // all elements to the iterator
    std::cout << "\n";                         // Output: 1, 2, 3, 7, 9, 10,
    // or from C++20 with Ranges:
    std::ranges::copy(data, out_it);
    std::cout << "\n";                         // Output: 1, 2, 3, 7, 9, 10,
}
```
```

**Listing 24.9** Iterator adapters change the behavior of operations.