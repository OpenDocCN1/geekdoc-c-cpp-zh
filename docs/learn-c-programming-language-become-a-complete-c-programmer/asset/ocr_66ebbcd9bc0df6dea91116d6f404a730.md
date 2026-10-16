Now objects of arbitrary types can be allocated from different Arenas as needed. For example:

```
extern Arena* Persistent; extern Arena* Shared;
void g(int i) {
X* p = new(Persistent) X(i); X* q = new(Shared) X(i); // ...
}
// Xinpersistent storage // Xinshared memory
```

# Section 11.2.4 Overloading new 285

Placing an object in an area that is not (directly) controlled by the standard free-store manager implies that some care is required when destroying the object. The basic mechanism for that is an explicit call of a destructor:

```
void destroy(X * p, Arena* a)
{
p->~X(); // call destructor
a->free(p); // free memory
}
```

Note that explicit calls of destructors should be avoided except in the implementation of resource management classes. Even most resource handles can be written using new and delete. However, it would be hard to implement an efficient general container along the lines of the standard-library vector (§4.4.1, §31.3.3) without using explicit destructor calls. A novice should think thrice before calling a destructor explicitly and also should ask a more experienced colleague before doing so.

See §13.6.1 for an example of how placement new can interact with exception handling. There is no special syntax for placement of arrays. Nor need there be, since arbitrary types can be allocated by placement new. However, an operator delete() can be defined for arrays (§11.2.3).

# 11.2.4.1 nothrow new

In programs where exceptions must be avoided (§13.1.5), we can use nothrow versions of new and delete. For example:

```
void f(int n)
{
int* p = new(nothrow) int[n]; // allocate n ints on the free store
if (p==nullptr) { // no memory available
// ... handle allocation error ...
}
// ...
operator delete(nothrow,p); // deallocate *p
}
```

That nothrow is the name of an object of the standard-library type nothrow_t that is used for disambiguation; nothrow and nothrow_t are declared in <new>. The functions implementing this are found in <new>: