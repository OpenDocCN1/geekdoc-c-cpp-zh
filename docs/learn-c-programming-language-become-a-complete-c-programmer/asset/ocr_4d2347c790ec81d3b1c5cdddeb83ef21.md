Using Ptr, the example is equivalent to:

```
void f3(T a) // checked
{
T v[200];
Ptr<T> p(&v[0],v,200);
p.operator--(0); // suffix: p-
p.operator*() = a; // run-time error:pout of range
p.operator++(); // prefix: ++p
p.operator*() = a; // OK
}
```

Completing class Ptr is left as an exercise. A pointer template that behaves correctly with respect to inheritability is presented in §27.2.2.

# 19.2.5 Allocation and Deallocation

Operator new (§11.2.3) acquires its memory by calling an operator new(). Similarly, operator delete frees its memory by calling an operator delete(). A user can redefine the global operator new() and operator delete() or define operator new() and operator delete() for a particular class.

Using the standard-library type alias size_t (§6.2.8) for sizes, the declarations of the global versions look like this:

```
void * operator new(size_t);
void* operator new[](size_t); void operator delete(void*,size_t); void operator delete[](void*,size_t);
```

```
// use for individual object // use for array
// use for individual object // use for array
```

// formore versions,see §11.2.4 That is, when new needs memory on the free store for an object of type X, it calls operator new(sizeof(X)). Similarly, when new needs memory on the free store for an array of N objects of type X, it calls operator new[](N*sizeof(X)). A new expression may ask for more memory than is indicated by N*sizeof(X), but it will always do so in terms of a number of characters (i.e., a number of bytes).

Replacing the global operator new() and operator delete() is not for the fainthearted and not recommended. After all, someone else might rely on some aspect of the default behavior or might even have supplied other versions of these functions.

A more selective, and often better, approach is to supply these operations for a specific class. This class might be the base for many derived classes. For example, we might like to have a class Employee provide a specialized allocator and deallocator for itself and all of its derived classes:

```
class Employee {
public:
// ...
```