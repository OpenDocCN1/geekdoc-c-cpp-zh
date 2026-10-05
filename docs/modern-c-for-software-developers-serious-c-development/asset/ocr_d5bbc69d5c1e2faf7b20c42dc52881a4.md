# std::shared_ptr

A single memory resource can be shared by several std::shared_ptr objects that wrap the resource. The application maintains an internal count of how many times the resource is shared by std::shared_ptr objects. When the shared pointer count reaches zero, the memory allocated to the shared resource is automatically freed.

Therefore std::shared_ptr allows copies of the shared smart pointer object to be made, but uses reference-counting to make sure that every smart pointer object is deleted only once. The memory allocated to the resource will be automatically destroyed when there are no smart pointer objects using the resource.

Each std::shared_ptr object maintains pointers to two shared memory areas: the memory area containing the shared data and a memory area containing the reference count.

When a new std::shared_ptr object is created, its constructor increases the reference count associated with the shared data by one.

When a shared_ptr goes out of scope, its destructor decrements the reference count to the shared resource by one. If the reference count becomes 0, this means that no shared_ptr object is associated with the shared memory. In this case, the destructor of the last shared pointer object deletes the shared memory.

# Shared Memory Pointers

The following is an example of shared memory pointer usage:

```
#include <iostream>
#include <string>
#include <memory>

void shared_user(std::string s, std::shared_ptr<double[]>& x) {
    std::cout << "share taken by: " << s;
    std::cout << " reference count: " << x.use_count() << std::endl;
```