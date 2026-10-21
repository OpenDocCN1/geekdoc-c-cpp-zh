The tracker is not used when we create a customer:

```
PmrCustomer c1{"Peter, Paul & Mary"};  // allocates with get_default_resource()
```

However, when we push a copy of the customer into the vector, the vector ensures that all the elements also use its polymorphic allocator. Therefore, the extended copy constructor of the PmrCustomer is called with the vector allocator as a second argument so that the element is initialized with the tracker.

```
std::pmr::vector<PmrCustomer> coll(&tracker);
...
PmrCustomer c1{"Peter, Paul & Mary"};  // allocates with get_default_resource()
coll.push_back(c1);                      // allocates with vector allocator (tracker)
```

The same happens if we move the customer into the vector, because the allocator of the vector (the tracker) is not interchangeable with the allocator of the customer (which uses the default resource):

```
std::pmr::vector<PmrCustomer> coll(&tracker);
...
PmrCustomer c1{"Peter, Paul & Mary"};  // allocates with get_default_resource()
...
coll.push_back(std::move(c1));           // copies (allocators not interchangeable)
```

If we also initialized the customer with the tracker, the move would work:

```
std::pmr::vector<PmrCustomer> coll(&tracker);
...
PmrCustomer c1{"Peter, Paul & Mary", &tracker};  // allocates with tracker
...
coll.push_back(std::move(c1));           // moves (same allocator)
```

The same is true if we do not use any tracker at all:

```
std::pmr::vector<PmrCustomer> coll;           // allocates with default resource
...
PmrCustomer c1{"Peter, Paul & Mary"};        // allocates with default resource
...
coll.push_back(std::move(c1));           // moves (same allocator)
```

# 29.3.3 Dealing with the Different Types

While using PmrCustomer with pmr types is quite nice, we have a problem: in general, programs use strings of type std::string. So how do we deal with using both std::string and std::pmr::string?

First, there is an explicit but no implicit conversion between different string types:

```
std::string s;
std::pmr::string t1{s};    // OK
std::pmr::string t2 = s;   // ERROR
s = t1;                    // ERROR
s = std::string(t1);       // OK
```