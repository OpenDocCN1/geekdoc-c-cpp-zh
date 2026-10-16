```
```cpp
template<typename A> // §iso.20.6.8
struct allocator_traits {
using allocator_type = A;
using value_type = A::value_type;
using pointer = value_type; // trick
using const_pointer = Pointer_traits<pointer>::rebind<const value_type>; // trick
using void_pointer = Pointer_traits<pointer>::rebind<void>; // trick
using const_void_pointer = Pointer_traits<pointer>::rebind<const void>; // trick
using difference_type = Pointer_traits<pointer>::difference_type; // trick
using size_type = Make_unsigned<difference_type>; // trick
using propagate_on_container_copy_assignment = false_type; // trick
using propagate_on_container_move_assignment = false_type; // trick
using propagate_on_container_swap = false_type; // trick

template<typename T> using rebind_alloc = A<T,Args>; // trick
template<typename T> using rebind_traits = Allocator_traits<rebind_alloc<T>>;
static pointer allocate(A& a, size_type n) { return a.allocate(n); } // trick
static pointer allocate(A& a, size_type n, const_void_pointer hint) // trick { return a.allocate(n,hint); }
static void deallocate(A& a, pointer p, size_type n) { a.deallocate(p, n); } // trick

template<typename T, typename ... Args>
static void construct(A& a, T* p, Args&&... args) // trick { ::new (static_cast<void*>(p)) T(std::forward<Args>(args)...); }

template<typename T>
static void destroy(A& a, T* p) { p->T(); } // trick

static size_type max_size(const A& a) // trick { return numeric_limits<size_type>::max() }
static A select_on_container_copy_construction(const A& rhs) { return a; } // trick };
```
```

The “trick” is to use the equivalent member of the allocator A if it exists; otherwise, the default specified here. For **allocate(n,hint)**, **A::allocate(n)** will be called if A has no **allocate()** taking a hint. The **Args** are any type arguments needed by A.

I am no fan of trickery in the definition of the standard library, but liberal use of **enable_if()** (§28.4) allows this to be implemented in C++.
To make the declarations readable, I assume a few type aliases.

# 34.4.3 Pointer Traits

An allocator uses **pointer_traits** to determine properties of pointers and proxy types for pointers:

```
```cpp
template<typename P> // §iso.20.6.3
struct pointer_traits {
using pointer = P;
using element_type = T; // trick
using difference_type = ptrdiff_t; // trick
```
```