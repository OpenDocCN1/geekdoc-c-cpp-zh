```
return *c + *d;
}

struct A { unsigned char a[32]; };
struct B { unsigned char b[16]; };
A a;
B *b = new (a.a + 8) B;          // a.a provides storage for *b
int *p = new (b->b + 4) int;     // b->b provides storage for *p
                               // a.a does not provide storage for *p (directly),
                               // but *p is nested within a (see below)
```

— end example]

4 An object a is nested within another object b if:

+   (4.1) — a is a subobject of b, or
+   (4.2) — b provides storage for a, or
+   (4.3) — there exists an object c where a is nested within c, and c is nested within b.

5 For every object x, there is some object called the complete object of x, determined as follows:

+   (5.1) — If x is a complete object, then the complete object of x is itself.
+   (5.2) — Otherwise, the complete object of x is the complete object of the (unique) object that contains x.

6 If a complete object, a member subobject, or an array element is of class type, its type is considered the most derived class, to distinguish it from the class type of any base class subobject; an object of a most derived class type or of a non-class type is called a most derived object.

7 A potentially-overlapping subobject is either:

+   (7.1) — a base class subobject, or
+   (7.2) — a non-static data member declared with the no_unique_address attribute (9.12.10).

8 An object has nonzero size if it

+   (8.1) — is not a potentially-overlapping subobject, or
+   (8.2) — is not of class type, or
+   (8.3) — is of a class type with virtual member functions or virtual base classes, or
+   (8.4) — has subobjects of nonzero size or bit-fields of nonzero length.

Otherwise, if the object is a base class subobject of a standard-layout class type with no non-static data members, it has zero size. Otherwise, the circumstances under which the object has zero size are implementation-defined. Unless it is a bit-field (11.4.10), an object with nonzero size shall occupy one or more bytes of storage, including every byte that is occupied in full or in part by any of its subobjects. An object of trivially copyable or standard-layout type (6.8) shall occupy contiguous bytes of storage.

9 Unless an object is a bit-field or a subobject of zero size, the address of that object is the address of the first byte it occupies. Two objects with overlapping lifetimes that are not bit-fields may have the same address if one is nested within the other, or if at least one is a subobject of zero size and they are of different types; otherwise, they have distinct addresses and occupy disjoint bytes of storage.32

[Example 2:

```
static const char test1 = 'x';
static const char test2 = 'x';
const bool b = &test1 != &test2;      // always true
```

— end example]

The address of a non-bit-field subobject of zero size is the address of an unspecified byte of storage occupied by the complete object of that subobject.

10 Some operations are described as implicitly creating objects within a specified region of storage. For each operation that is specified as implicitly creating objects, that operation implicitly creates and starts the lifetime of zero or more objects of implicit-lifetime types (6.8) in its specified region of storage if doing so would result in the program having defined behavior. If no such set of objects would give the program defined

> 32) Under the “as-if” rule an implementation is allowed to store two objects at the same machine address or not store an object at all if the program cannot observe the difference (6.9.1).