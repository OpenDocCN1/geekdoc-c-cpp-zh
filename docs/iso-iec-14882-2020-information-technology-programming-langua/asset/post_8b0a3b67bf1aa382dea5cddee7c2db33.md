
for an array object can specify array types that differ by the presence or absence of a major array bound (9.3.4.5). A violation of this rule on type identity does not require a diagnostic.

> [*Note 3:* Linkage to non-C++ declaration can be achieved using a *linkage-specification* (9.11). — *end note*]

**13** A declaration *D* names an entity *E* if

- (13.1) — *D* contains a *lambda-expression* whose closure type is *E*,
- (13.2) — *E* is not a function or function template and *D* contains an *id-expression*, *type-specifier*, *nested-name-specifier*, *template-name*, or *concept-name* denoting *E*, or
- (13.3) — *E* is a function or function template and *D* contains an expression that names *E* (6.3) or an *id-expression* that refers to a set of overloads that contains *E*.

> [*Note 4:* Non-dependent names in an instantiated declaration do not refer to a set of overloads (13.8.4). — *end note*]

**14** A declaration is an *exposure* if it either names a TU-local entity (defined below), ignoring

- (14.1) — the *function-body* for a non-inline function or function template (but not the deduced return type for a (possibly instantiated) definition of a function with a declared return type that uses a placeholder type (9.2.9.6)),
- (14.2) — the *initializer* for a variable or variable template (but not the variable’s type),
- (14.3) — friend declarations in a class definition, and
- (14.4) — any reference to a non-volatile const object or reference with internal or no linkage initialized with a constant expression that is not an odr-use (6.3),

or defines a constexpr variable initialized to a TU-local value (defined below).

> [*Note 5:* An inline function template can be an exposure even though explicit specializations of it are possibly usable in other translation units. — *end note*]

**15** An entity is *TU-local* if it is

- (15.1) — a type, function, variable, or template that
  - (15.1.1) — has a name with internal linkage, or
  - (15.1.2) — does not have a name with linkage and is declared, or introduced by a *lambda-expression*, within the definition of a TU-local entity,
- (15.2) — a type with no name that is defined outside a *class-specifier*, function body, or initializer or is introduced by a *defining-type-specifier* that is used to declare only TU-local entities,
- (15.3) — a specialization of a TU-local template,
- (15.4) — a specialization of a template with any TU-local template argument, or
- (15.5) — a specialization of a template whose (possibly instantiated) declaration is an exposure.

> [*Note 6:* A specialization can be produced by implicit or explicit instantiation. — *end note*]

**16** A value or object is *TU-local* if either

- (16.1) — it is, or is a pointer to, a TU-local function or the object associated with a TU-local variable, or
- (16.2) — it is an object of class or array type and any of its subobjects or any of the objects or functions to which its non-static data members or reference type refer is TU-local and is usable in constant expressions.

**17** If a (possibly instantiated) declaration of, or a deduction guide for, a non-TU-local entity in a module interface unit (outside the *private-module-fragment*, if any) or module partition (10.1) is an exposure, the program is ill-formed. Such a declaration in any other context is deprecated (D.8).

**18** If a declaration that appears in one translation unit names a TU-local entity declared in another translation unit that is not a header unit, the program is ill-formed. A declaration instantiated for a template specialization (13.9) appears at the point of instantiation of the specialization (13.8.5.1).

> [*Example 4:*]

Translation unit #1:

```cpp
export module A;
static void f() {}
inline void it() { f(); }        // error: is an exposure of f
static inline void its() { f(); } // OK
```

> declaration, or if they are separated by a non-bit-field declaration. It is not safe to concurrently update two bit-fields in the same struct if all fields between them are also bit-fields of nonzero width. — *end note*]

[*Example 1*: A class declared as

```cpp
struct {
  char a;
  int b:5,
      c:11,
      :0,
      d:8;
  struct {int ee:8;} e;
}
```

contains four separate memory locations: The member `a` and bit-fields `d` and `e.ee` are each separate memory locations, and can be modified concurrently without interfering with each other. The bit-fields `b` and `c` together constitute the fourth memory location. The bit-fields `b` and `c` cannot be concurrently modified, but `b` and `a`, for example, can be.

— *end example*]

## 6.7.2 Object model

The constructs in a C++ program create, destroy, refer to, access, and manipulate objects. An object is created by a definition (6.2), by a *new-expression* (7.6.2.8), by an operation that implicitly creates objects (see below), when implicitly changing the active member of a union (11.5), or when a temporary object is created (7.3.5, 6.7.7). An object occupies a region of storage in its period of construction (11.10.5), throughout its lifetime (6.7.3), and in its period of destruction (11.10.5).

> [*Note 1*: A function is not an object, regardless of whether or not it occupies storage in the way that objects do.
>
> — *end note*]

The properties of an object are determined when the object is created. An object can have a name (6.1). An object has a storage duration (6.7.5) which influences its lifetime (6.7.3). An object has a type (6.8). Some objects are polymorphic (11.7.3); the implementation generates information associated with each such object that makes it possible to determine that object’s type during program execution. For other objects, the interpretation of the values found therein is determined by the type of the *expressions* (7.6) used to access them.

Objects can contain other objects, called *subobjects*. A subobject can be a *member subobject* (11.4), a *base class subobject* (11.7), or an array element. An object that is not a subobject of any other object is called a *complete object*. If an object is created in storage associated with a member subobject or array element `e` (which may or may not be within its lifetime), the created object is a subobject of `e`’s containing object if:

- 1. the lifetime of `e`’s containing object has begun and not ended, and
- 2. the storage for the new object exactly overlays the storage location associated with `e`, and
- 3. the new object is of the same type as `e` (ignoring cv-qualification).

If a complete object is created (7.6.2.8) in storage associated with another object `e` of type “array of `N unsigned char`” or of type “array of `N std::byte`” (17.2.1), that array *provides storage* for the created object if:

- 1. the lifetime of `e` has begun and not ended, and
- 2. the storage for the new object fits entirely within `e`, and
- 3. there is no smaller array object that satisfies these constraints.

> [*Note 2*: If that portion of the array previously provided storage for another object, the lifetime of that object ends because its storage was reused (6.7.3). — *end note*]

[*Example 1*:

```cpp
template<typename ...T>
struct AlignedUnion {
  alignas(T...) unsigned char data[max(sizeof(T)...)];
};
int f() {
  AlignedUnion<int, char> au;
  int *p = new (au.data) int;       // OK, au.data provides storage
  char *c = new (au.data) char();   // OK, ends lifetime of *p
  char *d = new (au.data + 1) char();
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

- (4.1) — a is a subobject of b, or
- (4.2) — b provides storage for a, or
- (4.3) — there exists an object c where a is nested within c, and c is nested within b.

5 For every object x, there is some object called the complete object of x, determined as follows:

- (5.1) — If x is a complete object, then the complete object of x is itself.
- (5.2) — Otherwise, the complete object of x is the complete object of the (unique) object that contains x.

6 If a complete object, a member subobject, or an array element is of class type, its type is considered the most derived class, to distinguish it from the class type of any base class subobject; an object of a most derived class type or of a non-class type is called a most derived object.

7 A potentially-overlapping subobject is either:

- (7.1) — a base class subobject, or
- (7.2) — a non-static data member declared with the no_unique_address attribute (9.12.10).

8 An object has nonzero size if it

- (8.1) — is not a potentially-overlapping subobject, or
- (8.2) — is not of class type, or
- (8.3) — is of a class type with virtual member functions or virtual base classes, or
- (8.4) — has subobjects of nonzero size or bit-fields of nonzero length.

Otherwise, if the object is a base class subobject of a standard-layout class type with no non-static data members, it has zero size. Otherwise, the circumstances under which the object has zero size are implementation-defined. Unless it is a bit-field (11.4.10), an object with nonzero size shall occupy one or more bytes of storage, including every byte that is occupied in full or in part by any of its subobjects. An object of trivially copyable or standard-layout type (6.8) shall occupy contiguous bytes of storage.

9 Unless an object is a bit-field or a subobject of zero size, the address of that object is the address of the first byte it occupies. Two objects with overlapping lifetimes that are not bit-fields may have the same address if one is nested within the other, or if at least one is a subobject of zero size and they are of different types; otherwise, they have distinct addresses and occupy disjoint bytes of storage.32

[Example 2:

```cpp
static const char test1 = 'x';
static const char test2 = 'x';
const bool b = &test1 != &test2;      // always true
```

— end example]

The address of a non-bit-field subobject of zero size is the address of an unspecified byte of storage occupied by the complete object of that subobject.

10 Some operations are described as implicitly creating objects within a specified region of storage. For each operation that is specified as implicitly creating objects, that operation implicitly creates and starts the lifetime of zero or more objects of implicit-lifetime types (6.8) in its specified region of storage if doing so would result in the program having defined behavior. If no such set of objects would give the program defined

> 32) Under the “as-if” rule an implementation is allowed to store two objects at the same machine address or not store an object at all if the program cannot observe the difference (6.9.1).
