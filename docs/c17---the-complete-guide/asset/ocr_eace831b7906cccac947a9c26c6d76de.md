First, we allocate our own memory on the stack (using the new type std::byte):

```
// allocate some memory on the stack:
std::array<std::byte, 200000> buf;
```

Instead of std::byte you could also just use char.

Then, we initialize a monotonic_buffer_resource with this memory, passing its address and its size:

```
std::pmr::monotonic_buffer_resource pool{buf.data(), buf.size()};
```

Finally, we use a std::pmr::vector, which takes the memory resource for all its allocations:

```
std::pmr::vector<std::string> coll{&pool};
```

This declaration is just a shortcut for the following:

```
std::vector<std::string,
    std::pmr::polymorphic_allocator<std::string>> coll{&pool};
```

That is, we declare that the vector uses a polymorphic allocator, which can switch between different memory resources at runtime. The class monotonic_buffer_resource is derived from the class memory_resource and can therefore be used as a memory resource for a polymorphic allocator. So, by passing the address of our memory resource, we ensure that the vector uses our memory resource as a polymorphic allocator.

If we measure the allocated memory of this program, the output might become:

```
1000 allocations for 32000 bytes
```

The 18 allocations of the vector are no longer performed on the heap. Instead, our initialized buffer buf is used.

If the pre-allocated memory of 200,000 bytes is not sufficient, the vector will still allocate more memory on the heap. This happens because the monotonic_memory_resource uses the default allocator, which allocates memory with new as fallback.

# Not Allocating Memory At All

We can even avoid using heap memory at all by defining the element type of the std::pmr::vector to be std::pmr::string:

pmr/pmr2.cpp

```
#include <iostream>
#include <string>
#include <vector>
#include <array>
#include <cstdlib>  // for std::byte
#include <memory_resource>
#include "../lang/tracknew.hpp"

int main()
{
    TrackNew::reset();
```