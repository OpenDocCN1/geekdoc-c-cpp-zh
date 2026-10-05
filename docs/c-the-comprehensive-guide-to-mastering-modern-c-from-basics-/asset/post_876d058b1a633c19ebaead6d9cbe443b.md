
### Listing 24.9 Iterator adapters change the behavior of operations.

Every time the iterator out_it of type ostream_iterator is dereferenced and assigned something, it outputs it to cout. Between the elements, it prints a comma with a space ", ". So a *out_it = 42 results in the output 42., The copy algorithm from the <algorithm> header now performs exactly this assignment for all elements within the range data.begin() and data.end(). As a result, you get to see all elements on cout.

In the <iterator> header, there are other useful things for iterators. For example, you can reverse a range with reverse_iterator or use make_move_iterator to turn a copying algorithm into a moving one. For the exact functionalities, I refer you to the standard library reference, e.g., https://cppreference.com.

## 24.3 Allocators: Memory Issues

Containers constantly request new memory to store their elements. This can be a complex task, especially for noncontiguous containers like list or set. To give users the ability to intervene, each container is equipped with an allocator. If you do not specify one, it defaults to std::allocator<Elem>.

## Allocators Are an Expert Topic

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

```cpp
        std::cout << "allocate"<<(buf_.size())-current_ << "current_";
    if(current_ +add > buf_.size()) throw std::bad_alloc();
    char* result = buf_.data()+current_;
    current_ += add;
    return reinterpret_cast<T*>(result);
}
void deallocate(T* p, size_t count) {
    size_t t = sizeof(T)*count;
    std::cout << "deallocate"<<del << "\n";
    if(current_ == p && reinterpret_cast<T*>(buf_.data())) {
        std::cout << "...all free.\n";
        current_ = 0; // release everything again
    }
}

GobAllocator() : GobAllocator(1024) {}
explicit GobAllocator(size_t mx)
    buf_(mx, 0),
    current_(0) { }

private:
    std::vector<char> buf;
    size_t current_;
```

```cpp
int main() {
constexpr size_t CNT = 1*1000*1000;
using Gob = GobAllocator<int>;
try {
    Gob gob(sizeof(int)); // prepare allocator
    std::vector<int,Gob> data(gob); // get memory in one go
    data.reserve(CNT);
    for(int val=0; val < (int)CNT; ++val)
        data.push_back(val);
} catch(std::bad_alloc &ex) {
    std::cout << "Memory exhausted.\n";
}
```

## Listing 24.10 A simple allocator and its usage.

The GobAllocator acquires a vector<char> as a memory reservoir upon creation. It can allocate memory when the container requests it via allocate(), but it rarely deallocates it. The container requests this via deallocate(). Only if deallocate() wants to release all the requested memory will GobAllocator actually do something and releases all its memory for new requests.

Using current_, the GobAllocator keeps track of how much memory it has already managed. When it is asked to allocate memory for count objects via allocate(), it simply increases the current_ counter by the number of bytes these objects need. The old position is returned as data storage and converted into a raw pointer of the desired type. This means the container stores its elements here at this location.

It is also important to note that the allocator throws bad_alloc as an exception if it fails to obtain the requested memory. This then can be caught using try/catch. For example, omit data.reserve(CNT); in Listing_24.10 and observe how the GobAllocator runs out of space: the vector now wants to grow continuously and alternates between allocate() and deallocate() calls to request increasingly larger memory and release the old memory. However, this dumb allocator cannot do that and must eventually give up.

What this could theoretically be used for is reusing memory that has been obtained once.

Here, the memory from gob would be used twice completely, but only under the condition that data1 or data2 do not grow beyond cnt elements:

```cpp
Gob gob(CNT*sizeof(int)); // prepare common allocator
{
  std::vector<int,Gob> data1(gob);
  data1.reserve(CNT);
  // ...
```

```cpp
  std::vector<int,Gob> data2(gob);
data2.reserve(CNT);
// ...
```

All in all, this simple allocator is quite useless in practice. But at least it shows you how to equip a container with an allocator.

## All Containers Support Allocators

All containers of the standard library use an allocator. If you do not specify one, the standard library uses `std::allocator<Elem>`. You can specify your own by passing its type as a template parameter. In addition, you can optionally pass an instance of your allocator to the constructor or let the container create a new one if you do not want to.

The classical allocators described here have a weakness: two containers that are essentially the same but have different allocators are of different types, because an allocator is part of the container type. This means in practice that you cannot assign between them.

The solution is containers with `polymorphic allocators`. Two containers that use these are of the same type even if they use different allocators. Therefore, since C++17, all containers are also available in the `std::pmr` namespace—for example, `std::pmr::vector` (polymorphic memory resource).

Ahead, I will omit the allocator as template argument and pass it as constructor parameter for all containers, as well as pmr variant.

## 24.4 Container Commonalities

When designing this part of the standard library, great care was taken to provide a common interface for the containers where it makes sense. I do not list the special cases—they are explained with the specific container—but only give a rough overview:

- begin() end()
All containers offer these two functions to get iterators. Among other things, this allows you to use them in the range-based for loop, because they also exist as free functions.

- size() empty() std::size()
Get the number of elements in any container. Since C++17, they also exist as free functions, and from C++20, there is the free function ssize(), which returns size() as signed. This avoids warnings about comparisons between signed and unsigned in statements like (int i=0; i<cont.size(); ++i). Just write i<ssize(cont).

- resize() reserve() clear()
You can resize or shrink sequence-based containers (except array) with a single call. vector and the unordered containers can be informed about how many elements you intend to store approximately. This saves administrative effort when actually inserting.

- operator[] at() data()
Read and write at arbitrary positions of a container with cont[where] or cont.at(where). Not all containers support this. Sequence-based ones require a number for where, while associative ones need the data type you chose as the key. With data(), you can access the contiguous memory of elements in some containers. This is useful for C functions, among other things. data() is also available as a free function.

- insert() insert_range() emplace()
Use these to insert or delete elements at arbitrary positions. Note that vector can do this, but it is slow. With insert(), the element already exists and is copied (or moved in the case of temp-values), while with
