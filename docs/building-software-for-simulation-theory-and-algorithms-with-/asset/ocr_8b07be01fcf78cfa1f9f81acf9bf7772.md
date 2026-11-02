```
```cpp
unsigned cap_, size_;
T* b;
// Adds the specified capacity to the bag.
void enlarge(unsigned adjustment)
{
    cap_ = cap_ + adjustment;
    T* rb = new T[cap_];
    for (unsigned int i = 0; i < size_; i++)
        rb[i] = b[i];
    delete [] b;
    b = rb;
}
};
}; // end of namespace

#endif
```
```

Only a handful of bags are actually needed at any moment, and it is wasteful to create separate bags for each atomic model and to create and destroy bags while routing an event. The simulator can reduce its use of memory by having a cache of bags that are reused as needed.

This cache is implemented by the *ObjectPool* class, which stores a collection of reusable objects. It has two methods plus a constructor and a destructor. The constructor creates an initial pool of objects. The *make_obj* method gets an object from the pool and returns it, or, if the pool is empty, creates a new object. The *destroy_obj* method puts the supplied object into the pool. It is the responsibility of the caller to ensure that the object is restored to its initial state before being returned for reuse. The destructor deletes the pool. The code for the *ObjectPool* is listed below.

# **Implementation of the ObjectPool Class**

```
```cpp
#ifndef __adevs_object_pool_h_
#define __adevs_object_pool_h_
#include "adevs_bag.h"

namespace adevs
{

template <class T> class object_pool
{
public:
    // Construct a pool with a specific initial population
    object_pool(unsigned int pop = 0):pool()
    {
        for (unsigned int i = 0; i < pop; i++)
            pool.insert(new T());
```
```