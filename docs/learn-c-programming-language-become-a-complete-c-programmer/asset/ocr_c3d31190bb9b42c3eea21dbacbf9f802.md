# ### 3.3.3 Resource Management

By defining constructors, copy operations, move operations, and a destructor, a programmer can provide complete control of the lifetime of a contained resource (such as the elements of a container). Furthermore, a move constructor allows an object to move simply and cheaply from one scope to another. That way, objects that we cannot or would not want to copy out of a scope can be simply and cheaply moved out instead. Consider a standard-library **thread** representing a concurrent activity (§5.3.1) and a **Vector** of a million **doubles**. We can’t copy the former and don’t want to copy the latter.

```
```cpp
std::vector<thread> my_threads;

Vector init(int n) {
    thread t {heartbeat}; // run heartbeat concurrently (on its own thread)
    my_threads.push_back(move(t)); // move t into my_threads
    // ... more initialization ...

    Vector vec(n);
    for (int i=0; i<vec.size(); ++i) vec[i] = 777;
    return vec; // move res out of init()
}

auto v = init(); // start heartbeat and initialize v
```
```

This makes resource handles, such as **Vector** and **thread**, an alternative to using pointers in many cases. In fact, the standard-library “smart pointers,” such as **unique_ptr**, are themselves resource handles (§5.2.1).

I used the standard-library **vector** to hold the **threads** because we don’t get to parameterize **Vector** with an element type until §3.4.1.

In very much the same way as **new** and **delete** disappear from application code, we can make pointers disappear into resource handles. In both cases, the result is simpler and more maintainable code, without added overhead. In particular, we can achieve *strong resource safety*; that is, we can eliminate resource leaks for a general notion of a resource. Examples are **vectors** holding memory, **threads** holding system threads, and **fstreams** holding file handles.

# ### 3.3.4 Suppressing Operations

Using the default copy or move for a class in a hierarchy is typically a disaster: given only a pointer to a base, we simply don’t know what members the derived class has (§3.2.2), so we can’t know how to copy them. So, the best thing to do is usually to *delete* the default copy and move operations, that is, to eliminate the default definitions of those two operations:

```
```cpp
class Shape {
public:
    Shape(const Shape&) = delete;
```
```