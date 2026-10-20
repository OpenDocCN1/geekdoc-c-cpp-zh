At the end we are in the same state as before using move semantics but something significant has changed: we saved six allocations and releases of memory. All unnecessary memory allocations no longer took place:

+   - Allocations for inserting a temporary object into the collection
+   - Allocations for inserting a named object into the collection, when we use std::move() to signal that we no longer need the value
+   - Allocations for assigning a temporary vector with all its elements

In the second case, the optimization was done with our help. By adding std::move(), we had to say that we no longer needed the value of s there. All other optimizations happened because the compiler knows that an object is about to die, meaning that it can call the optimized implementation, which uses move semantics.

This means that returning a vector of strings and assigning it to an existing vector is no longer a performance issue. We can use a vector of strings naively like an integral type and get much better performance. In practice, recompiling code with move semantics can improve speed by 10% to 40% (depending on how naive the existing code was).

# 1.2 Implementing Move Semantics

Let us use the previous example to see where and how move semantics is implemented.

Before move semantics was implemented, class std::vector<> had only one implementation of push_back() (the declaration of vector is simplified here):

```
template<typename T>
class vector {
public:
    ...
    // insert a copy of elem:
    void push_back (const T& elem);
    ...
};
```

There was only one way to pass an argument to push_back() binding it to a const reference. push_back() is implemented in a way that the vector creates an internal copy of the passed argument without modifying it.

Since C++11, we have a second overload of push_back():

```
template<typename T>
class vector {
public:
    ...
    // insert a copy of elem:
    void push_back (const T& elem);

    // insert elem when the value of elem is no longer needed:
    void push_back (T&& elem);
    ...
};
```