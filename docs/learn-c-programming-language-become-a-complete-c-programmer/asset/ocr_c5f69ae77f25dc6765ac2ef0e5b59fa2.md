elements. For implementations where entering a try-block incurs a cost, it may be worthwhile to add a test if (n) before the try to explicitly handle the (very common) empty vector case.

The main part of this constructor is a repeat of the implementation of std::uninitialized_fill():

```
template<class For, class T>
void uninitialized_fill(For beg, For end, const T& x)
{
For p; try {
for (p=beg; p!=end; ++p)
::new(static_cast<void *>(&*p)) T(x); // construct copy of x in *p (§11.2.4) }
catch (...) {
for (For q = beg; q!=p; ++q)
(&*q)->~T(); // destroy element (§11.2.4)
throw; // rethrow (§13.5.2.1)
}
}
```

The curious construct &*p takes care of iterators that are not pointers. In that case, we need to take the address of the element obtained by dereference to get a pointer. Together with the explicitly global ::new, the explicit cast to void* ensures that the standard-library placement function (§17.2.4) is used to invoke the constructor, and not some user-defined operator new() for T*. The calls to alloc.construct() in the vector constructors are simply syntactic sugar for this placement new. Similarly, the alloc.destroy() call simply hides explicit destruction (like (&*q)->~T()). This code is operating at a rather low level where writing truly general code can be difficult.

Fortunately, we don’t have to invent or implement uninitialized_fill(), because the standard library provides it (§32.5.6). It is often essential to have initialization operations that either complete successfully, having initialized every element, or fail, leaving no constructed elements behind. Consequently, the standard library provides uninitialized_fill(), uninitialized_fill_n(), and uninitialized_copy() (§32.5.6), which offer the strong guarantee (§13.2).

The uninitialized_fill() algorithm does not protect against exceptions thrown by element destructors or iterator operations (§32.5.6). Doing so would be prohibitively expensive and probably impossible.

The uninitialized_fill() algorithm can be applied to many kinds of sequences. Consequently, it takes a forward iterator (§33.1.2) and cannot guarantee to destroy elements in the reverse order of their construction.

Using uninitialized_fill(), we can simplify our constructor:

```
template<class T, class A>
vector<T,A>::vector(size_type n, const T& val, const A& a) // still a bit messy
```