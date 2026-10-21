of memory are, so that more elements are located close to each other. The details of these algorithms are implementation-specific.

Of course, this output is special because we create the elements in the order that they are sorted inside the container. Thus, in practice, if you create objects with random values, the elements will not be located sequentially one after the other (in different chunks of memory). However, they are still located close to each other and that is important for good performance when dealing with the elements of this container.

Note also that we do not look at how memory for the element values is arranged. Here, use of the small string optimization usually causes no memory to be allocated for the elements. However, as soon as we enlarge the string values, the pool also tries to place those together. Note that the pool manages different chunks of memory for different allocated sizes. That is, in general, the elements are located next to each other and the string values for elements of the same string size are also located close to each other.

# monotonic_buffer_resource

The class monotonic_buffer_resource also provides the ability to place all memory in big chunks of memory. However, it has two other abilities:

+   - You can pass a buffer to be used as memory. In particular, this can be memory allocated on the stack.
+   - The memory resource never deallocates until the resource as a whole is deallocated.

That is, this memory resource is very fast because deallocation is a no-op and you skip the need to track deallocated memory for further use. Whenever there is a request to allocate memory, the resource just returns the next free piece of memory until all memory is exhausted.

Note that objects are still destructed. Only their memory is not freed. If you delete objects, which usually deallocates their memory, the deallocation has no effect.

This resource is recommended if you either have no deletes or if you have enough memory to waste (not reusing memory that was previously used by another object).

We have already seen applications of monotonic_buffer_resource in our first motivating examples, where we passed memory allocated on the stack to the pool:

```
std::array<std::byte, 200000> buf;
std::pmr::monotonic_buffer_resource pool{buf.data(), buf.size()};
```

You can also use this pool to allow any memory resource to skip deallocations (optionally passing an initial size). By default, this would apply to the default memory resource, which is new_delete_resource() by default. That is, with

```
// use default memory resource but skip deallocations as long as the pool lives:
{
    std::pmr::monotonic_buffer_resource pool;

    std::pmr::vector<std::pmr::string> coll{&pool};
    for (int i=0; i < 100; ++i) {
        coll.emplace_back("just a non-SSO string");
    }
    coll.clear();  // destruction but no deallocation
} // deallocates all allocated memory
```