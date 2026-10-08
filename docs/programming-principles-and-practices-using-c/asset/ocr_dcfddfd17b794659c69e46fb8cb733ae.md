solution is simple and general. Using resource handles simplifies code and eliminates a major source of errors. Compared to the direct use of pointers, the run-time over-head of using such handles is nothing, or very minor and predictable.

# 19.5.6  RAIL for **vector**

Even using a smart pointer, such as **unique_ptr**, may seem to be a bit ad hoc. How can we be sure that we have spotted all pointers that require protection? How can we be sure that we have released all pointers to objects that should not be destroyed at the end of a scope? Consider **reserve()** from §19.3.7:

```
template<typename T, typename A>
void vector<T,A>::reserve(int newalloc)
{
            if (newalloc<=space) return;     // never decrease allocation
            T* p = alloc.allocate(newalloc);   // allocate new space
            for (int i=0; i<sz; ++i) alloc.construct(&p[i],elem[i]);   // copy
            for (int i=0; i<sz; ++i) alloc.destroy(&elem[i]);   // destroy
            alloc.deallocate(elem,space);   // deallocate old space
            elem = p;
            space = newalloc;
}
```

Note that the copy operation for an old element, **alloc.construct(&p[i],elem[i])**, might throw an exception. So, **p** is an example of the problem we warned about in §19.5.1. Ouch! We could apply the **unique_ptr** solution. A better solution is to step back and realize that “memory for a **vector**” is a resource; that is, we can de-fine a class **vector_base** to represent the fundamental concept we have been using all the time, the picture with the three elements defining a **vector**’s memory use:

![](bbox=[0.21, 0.68, 0.83, 0.8])

In code, that is (after adding the allocator for completeness)

```
template<typename T, typename A>
struct vector_base {
    A alloc;   // allocator
    T* elem;   // start of allocation
```