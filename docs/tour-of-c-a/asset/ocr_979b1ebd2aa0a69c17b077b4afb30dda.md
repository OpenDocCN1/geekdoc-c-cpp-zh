+   • Don’t retain a pointer to a local object after the object goes out of scope. In particular, never return a pointer to a local object from a function or store a pointer of uncertain provenance in a long-lived data structure. Systematic use of containers and algorithms (Chapter 12, Chapter 13) often saves us from employing programming techniques that make it hard to avoid problems.

+   • Use owning pointers to objects allocated on the free store.

+   • Pointers to static objects (e.g., global variables) can’t dangle.

+   • Leave pointer arithmetic to the implementation of resource handles (such as vectors and unordered_maps).

+   • Remember that string_views and spans are kinds of non-owning pointers.

# 15.2.1 unique_ptr and shared_ptr

One of the key tasks of any nontrivial program is to manage resources. A resource is something that must be acquired and later (explicitly or implicitly) released. Examples are memory, sockets, threads and file handles. For a long-running program, failing to release a resource in a timely manner (a “leak”) can cause severe performance degradation (§12.7) and possibly even a miserable crash. Even for short programs, a leak can become an embarrassment, by causing a resource shortage increasing the run time by orders of magnitude.

The standardlibrary components are designed not to leak resources. To do this, they rely on the basic language support for resource management using constructor/destructor pairs to ensure that a resource doesn’t outlive an object responsible for it. Using of constructor/destructor pair in Vector to manage the lifetime of elements is an example (§5.2.2) and all standard-library containers are implemented in similar ways. Importantly, this approach interacts correctly with error exceptions. For example, this technique is used for the standard-library lock classes:

Click here to view code image

```
mutex m; // used to protect access to shared data
void f()
{
    scoped_lock lock(m); // Acquire the mutex m
    // ... manipulate shared data ...n}
```

A thread will not unlock lock()’s constructor has acquired the mutex (§18.3). The corresponding destructor releases the mutex. In this example, scoped_lock releases the mutex through the thread of control unless f() (through a return, or “falling off the end of the exception”).

This is an example of RAII (“Resource Acquisition Is Initialization” technique); (§5.2.2). RAII is the idiomatic handling of resources in C++. Containers (such as vector and map, string, and iostream) manage their resources (such as file handles and buffers) similarly.

The examples far take care of objects in a scope, releasing the resources they acquire from the scope, but what about objects allocated on the free store? In <memory>, the standard library provides two “smart pointers” to help manage objects on the free