# ISO/IEC 14882:2017(E)

```
void g() {
  char* buf = new char[sizeof(X)]; // rare, specialized use:
  X* p = new(buf)(X(222)); // use buf[] and initialize
  f(p);
  p->~X(); // cleanup
} // end note;
```

16 Once a destructor is invoked for an object, the object no longer exists; the behavior is undefined if the destructor is invoked for an object whose lifetime has ended (6.8). [Example: If the destructor for an automatic object is implicitly invoked, and the block is subsequently left in a manner that would ordinarily invoke destruction of the object, the behavior is undefined. — end example]

17 [Note: The notation for explicit call of a destructor can be used for any scalar type (8.2.4). Allowing this makes possible to write code without knowing if a destructor exists for a given type. For example:

```
typedef int I;
I* p = p->~I();
// end note;
```

# 15.5 Free store [class.free]

+   1 Any allocation function for a class τ is a static member (even if not explicitly declared static).

+   2 [Example:

```
class Arena;
struct B {
  void* operator(std::size_t, Arena*);
  struct D1 : B {
  };
  struct D1[i];
  };
}
```

```
Arena* ap;
void foo(int i) {
  new (ap) D1(); // calls ::operator new(std::size_t, Arena*)
  new D1[i]; // calls ::operator new[](std::size_t)
  new D1{i}; // ill-formed: ::operator new(std::size_t) hidden
} // end example
```

3 When a destructor is invoked by a delete-expression (8.3.5, for non-array objects or operator delete[] (for arrays)) is (implicitly) called to reclaim the storage occupied by the object (6.7.4.2).

4 Class-specific deallocation lookup is a part of general deallocation lookup (8.3.5) and occurs as follows. If the delete-expression is used to delete a class object type has a virtual destructor, the deallocation function is selected at the point of definition of the type's virtual destructor (15.4).¹⁸ Otherwise, if the delete-expression is used to delete an object class T or array thereof, the static and dynamic types of the object shall be identical and the deallocation function's name is looked up in the scope of T. If this lookup fails to find a name, general deallocation function

> ¹⁸ A similar comparison is not needed for the array version of operator delete because 8.3.5 requires that in this situation, the static type of the object to be deleted be the same as its dynamic type.