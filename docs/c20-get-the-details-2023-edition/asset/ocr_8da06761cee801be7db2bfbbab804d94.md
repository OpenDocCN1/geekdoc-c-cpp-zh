![](bbox=[0.116, 0.116, 0.886, 0.286])

The first ten error lines of GCC

The next issue is more subtle.

# ### 5.1.8.2 Unified Lookup Rules

Assume you want to implement a generic function that calls begin on a given container. The question is if the function call begin on a container should assume a free begin function or a member function begin.

A free begin function versus a member function begin

```
```cpp
// begin.cpp

#include <cstddef>
#include <iostream>
#include <ranges>

struct ContainerFree {
    ContainerFree(std::size_t len): len_(len), data_(new int[len]){}
    size_t len_;
    int* data_;
};
int* begin(const ContainerFree& conFree) {
    return conFree.data_;
}

struct ContainerMember {
    ContainerMember(std::size_t len): len_(len), data_(new int[len]){}
    int* begin() const {
        return data_;
    }
    size_t len_;
    int* data_;
};
```
```