# 24.3 Allocators: Memory Issues

Containers constantly request new memory to store their elements. This can be a complex task, especially for noncontiguous containers like list or set. To give users the ability to intervene, each container is equipped with an allocator. If you do not specify one, it defaults to std::allocator<Elem>.

# Allocators Are an Expert Topic

> I recommend that you use std::allocator and do not implement your own allocator. If you do, use ones from the Boost project or other major providers. The concept of allocators implemented in the current standard library is much debated and does not make all experts happy. You should not bother delving deeply into this subject unless you really have to.

To show you how to use allocators, I will now define a very simple allocator. There are much more sophisticated ones, but for general and specific situations.

```
// https://godbolt.org/z/3dYh6n5f
#include <set>
#include <vector>
#include <iostream>

template<class T> class GobAllocator {
public:
    using value_type = T;
    T* allocate(size_t count) {
        size_t add = sizeof(T)*count;
```