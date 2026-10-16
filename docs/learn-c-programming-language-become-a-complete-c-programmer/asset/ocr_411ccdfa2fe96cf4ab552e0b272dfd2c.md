The curious **rebind** template is an archaic alias. It should have been:

```
template<typename U>
using other = allocator<U>;
```

However, **allocator** was defined before such aliases were supported by C++. It is provided to allow an allocator to allocate objects of arbitrary type. Consider:

```
using Link_alloc = typename A::template rebind<Link>::other;
```

If **A** is an **allocator**, then **rebind<Link>::other** is an alias for **allocator<Link>**. For example:

```
template<typename T, typename A = allocator<T>>
class list {
private:

class Link { /* ... */ };
using Link_alloc = typename A::template rebind<Link>::other; // allocator<Link>
Link_alloc a; // link allocator
A alloc; // list allocator
// ...
};
```

A more restricted specialization of **allocator<T>** is provided:

```
template<>
class allocator<void> {
public:

typedef void * pointer;
typedef const void* const_pointer;
typedef void value_type;
template<typename U> struct rebind { typedef allocator<U> other; };
};
```

This allows us to avoid special cases: We can mention **allocator<void>** as long as we don’t dereference its pointers.

# 34.4.2 Allocator Traits

The allocators are “wired together” using **allocator_traits**. A property of an allocator, say, its **pointer** type, is found in its trait: **allocator_traits<X>::pointer**. As usual, the traits technique is used so that I can build an allocator for a type that does not have member types matching the requirements of an allocator, such as **int**, and a type designed without any thought of allocators.

Basically, **allocator_traits** provide defaults for the usual set of type aliases and allocator functions. Compared to the default **allocator** (§34.4.1), **address()** is missing and **select_on_container_copy_construction()** is added: