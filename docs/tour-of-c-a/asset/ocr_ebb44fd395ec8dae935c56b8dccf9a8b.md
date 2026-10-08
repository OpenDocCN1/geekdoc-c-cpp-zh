+   - A unordered_map requires an equality function (the default is ==); it does not maintain an order among its elements.

Given a good function, unordered_map is much faster than a map for large containers. However, the worst-case behavior of an unordered_map with a poor hash function is far worse than that of a map.

# 12.7 Allocators

By default, standard-library containers allocate space using new. Operators new and delete provide a free store (also called dynamic memory) that can hold objects of arbitrary size and user-controlled lifetimes. Therefore, the standard-library containers offer the opportunity to install allocators with semantics we need. This has been used to address a wide variety of concerns related to performance (e.g., pool allocators), security (allocators that clean-up memory as part of deletion), per-thread allocation, and non-uniform memory allocators (allocating in specific memories with pointer types to). This is not the place to discuss these important, but very specialized and advanced techniques. However, I will give one example motivated by a real-world problem for which a pool allocator was the

An important, long-running system used an event queue (see §18.4) using as events that were passed as shared_ptrs. That way, the user of an event implicitly deleted it:

Click here to view code image

```
struct Event {
    vector<int> data = vector<int>(52);
};

list<shared_ptr<Event>> q;

void producer() {
    for (int n = 0; n!=nLTS; ++n) {
        lock_guard lock(m);
        q.push_back(make_shared<Event>());
        cv.notify_one();
    }
}
```

From a logical point of view this worked nicely. It is logically so, the code is robust and maintainable. Unfortunately, this led to memory fragmentation. After 100,000 events had been passed among 16 producers and 4 consumers, more than 6GB of memory had been consumed.

The traditional solution to fragmentation problems is to rewrite the code to use a pool allocator. A pool allocator manages objects of a single fixed size and allocates space for many objects at time, rather than using individual allocations. Fortunately, C++ offers direct support for that. The pool allocator is defined in the pmr ("polymorphic memory resource")

subnamespace of std.

Click here to view code image

```
pmr::synchronized_pool_resource;
```

Il make a pool