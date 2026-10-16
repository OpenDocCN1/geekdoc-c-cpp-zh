to the functions defined in <new>, a user can define operator new(), etc., for a specific class (§19.2.5). Class members operator new(), etc., are found and used in preference to the ones from <new> according to the usual scope rules.

# 11.2.4 Overloading new

By default, operator new creates its object on the free store. What if we wanted the object allocated elsewhere? Consider a simple class:

```
class X {
public:
X(int);
// ...
};
```

We can place objects anywhere by providing an allocator function (§11.2.3) with extra arguments and then supplying such extra arguments when using new:

```
void* operator new(size_t, void* p) { return p; } // explicit placement operator
void* buf = reinterpret_cast<void*>(0xF00F); // significant address X* p2 = new(buf) X; // construct an X at buf; // invokes: operator new(sizeof(X),buf)
```

Because of this usage, the new(buf) X syntax for supplying extra arguments to operator new() is known as the placement syntax. Note that every operator new() takes a size as its first argument and that the size of the object allocated is implicitly supplied (§19.2.5). The operator new() used by the new operator is chosen by the usual argument matching rules (§12.3); every operator new() has a size_t as its first argument.

The “placement” operator new() is the simplest such allocator. It is defined in the standard header <new>:

```
void* operator new (size_t sz, void* p) noexcept; void* operator new[](size_t sz, void* p) noexcept;
// place object of size sz at p // place object of size sz at p
void operator delete (void* p, void*) noexcept; // if (p) make *p invalid
void operator delete[](void* p, void*) noexcept; // if (p) make *p invalid
```

The “placement delete” operators do nothing except possibly inform a garbage collector that the deleted pointer is no longer safely derived (§34.5).

The placement new construct can also be used to allocate memory from a specific arena:

```
class Arena {
public:
virtual void* alloc(size_t)=0;
virtual void free(void*)=0;
// ...
};
```

```
void* operator new(size_t sz, Arena* a)
{
return a->alloc(sz);
}
```