```
```cpp
std::cout << number << " ";
std::cout << std::endl;
}
```
```

**Listing 6.10** The simplest iteration uses a range based “for” loop.

Here, all elements are output sequentially: 1 4 9 16 25. Alternatively, you can also access the elements by index. Don't forget that the counting (almost always in C++) starts at zero. You can use `size()` to check how many elements are in the vector.

Note that I wrote `std::vector` here instead of `std::vector<int>` because the compiler deduces `<int>` from the constructor arguments since C++17.

```
```cpp
// https://godbolt.org/z/xCKM7v1Eo
#include <vector>
#include <iostream>                         // cout, endl
int main() {
    std::vector qs{1,4,9,16,25};
    for(unsigned idx=0; idx<qs.size(); ++idx) // size returns the count
        std::cout << qs[idx] << " ";         // [idx] or at(idx) gets an element
    std::cout << std::endl;
}
```
```

**Listing 6.11** Accessing the elements by index.

In C++, however, you should use iterators instead of an index. They can be used more widely, may be easier for the compiler to handle, and, above all, are the same for all containers.

```
```cpp
// https://godbolt.org/z/1WG8zvhYe
#include <vector>
#include <iostream>                         // cout, endl
int main() {
    std::vector qs{1,4,9,16,25};
    for(auto it = qs.begin(); it!=qs.end(); ++it) // between begin() and end()
        std::cout << *it << " ";                  // with *it you get from the element
    std::cout << std::endl;
}
```
```

**Listing 6.12** The use of iterators for a loop.

Just like containers, *iterators* are a general idea. They work closely with containers and are also explained in detail in Chapter 24. For now, I will summarize them for you in the shortest possible way: