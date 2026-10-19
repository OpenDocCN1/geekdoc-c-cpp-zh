

behavior, the behavior of the program is undefined. If multiple such sets of objects would give the program defined behavior, it is unspecified which such set of objects is created.

[Note 3: Such operations do not start the lifetimes of subobjects of such objects that are not themselves of implicit-lifetime types. — end note]

11 Further, after implicitly creating objects within a specified region of storage, some operations are described as producing a pointer to a suitable created object. These operations select one of the implicitly-created objects whose address is the address of the start of the region of storage, and produce a pointer value that points to that object, if that value would result in the program having defined behavior. If no such pointer value would give the program defined behavior, the behavior of the program is undefined. If multiple such pointer values would give the program defined behavior, it is unspecified which such pointer value is produced.

12 [Example 3:

```
#include <cstdlib>
struct X { int a, b; };
X *make_x() {
    // The call to std::malloc implicitly creates an object of type X
    // and its subobjects a and b, and returns a pointer to that X object
    // (or an object that is pointer-interconvertible (6.8.3) with it),
    // in order to give the subsequent class member access operations
    // defined behavior.
    X *p = (X*)std::malloc(sizeof(struct X));
    p->a = 1;
    p->b = 2;
    return p;
}
```

— end example]

13 An operation that begins the lifetime of an array of char, unsigned char, or std::byte implicitly creates objects within the region of storage occupied by the array.

[Note 4: The array object provides storage for these objects. — end note]

Any implicit or explicit invocation of a function named operator new or operator new[] implicitly creates objects in the returned region of storage and returns a pointer to a suitable created object.

[Note 5: Some functions in the C++ standard library implicitly create objects (20.10.9.3, 20.10.12, 21.5.3, 26.5.3). — end note]

## 6.7.3 Lifetime [basic.life]

1 The lifetime of an object or reference is a runtime property of the object or reference. A variable is said to have vacuous initialization if it is default-initialized and, if it is of class type or a (possibly multi-dimensional) array thereof, that class type has a trivial default constructor. The lifetime of an object of type T begins when:

- (1.1) — storage with the proper alignment and size for type T is obtained, and
- (1.2) — its initialization (if any) is complete (including vacuous initialization) (9.4),

except that if the object is a union member or subobject thereof, its lifetime only begins if that union member is the initialized member in the union (9.4.2, 11.10.3), or as described in 11.5 and 11.4.5.3, and except as described in 20.10.10.2. The lifetime of an object o of type T ends when:

- (1.3) — if T is a non-class type, the object is destroyed, or
- (1.4) — if T is a class type, the destructor call starts, or
- (1.5) — the storage which the object occupies is released, or is reused by an object that is not nested within o (6.7.2).

2 The lifetime of a reference begins when its initialization is complete. The lifetime of a reference ends as if it were a scalar object requiring storage.

3 [Note 1: 11.10.3 describes the lifetime of base and member subobjects. — end note]

4 The properties ascribed to objects and references throughout this document apply for a given object or reference only during its lifetime.

[Note 2: In particular, before the lifetime of an object starts and after its lifetime ends there are significant restrictions on the use of the object, as described below, in 11.10.3 and in 11.10.5. Also, the behavior of an object under

construction and destruction is possibly not the same as the behavior of an object whose lifetime has started and not ended. 11.10.3 and 11.10.5 describe the behavior of an object during its periods of construction and destruction. — end note]

5 A program may end the lifetime of any object by reusing the storage which the object occupies or by explicitly calling a destructor or pseudo-destructor (7.5.4.4) for the object. For an object of a class type, the program is not required to call the destructor explicitly before the storage which the object occupies is reused or released; however, if there is no explicit call to the destructor or if a delete-expression (7.6.2.9) is not used to release the storage, the destructor is not implicitly called and any program that depends on the side effects produced by the destructor has undefined behavior.

6 Before the lifetime of an object has started but after the storage which the object will occupy has been allocated33 or, after the lifetime of an object has ended and before the storage which the object occupied is reused or released, any pointer that represents the address of the storage location where the object will be or was located may be used but only in limited ways. For an object under construction or destruction, see 11.10.5. Otherwise, such a pointer refers to allocated storage (6.7.5.5.2), and using the pointer as if the pointer were of type void* is well-defined. Indirection through such a pointer is permitted but the resulting lvalue may only be used in limited ways, as described below. The program has undefined behavior if:

- (6.1) — the object will be or was of a class type with a non-trivial destructor and the pointer is used as the operand of a delete-expression,
- (6.2) — the pointer is used to access a non-static data member or call a non-static member function of the object, or
- (6.3) — the pointer is implicitly converted (7.3.12) to a pointer to a virtual base class, or
- (6.4) — the pointer is used as the operand of a static_cast (7.6.1.9), except when the conversion is to pointer to cv void, or to pointer to cv void and subsequently to pointer to cv char, cv unsigned char, or cv std::byte (17.2.1), or
- (6.5) — the pointer is used as the operand of a dynamic_cast (7.6.1.7).

[Example 1:

```
#include <cstdlib>

struct B {
    virtual void f();
    void mutate();
    virtual ~B();
};

struct D1 : B { void f(); };
struct D2 : B { void f(); };

void B::mutate() {
    new (this) D2;    // reuses storage — ends the lifetime of *this
    f();              // undefined behavior
    ... = this;       // OK, this points to valid memory
}

void g() {
    void* p = std::malloc(sizeof(D1) + sizeof(D2));
    B* pb = new (p) D1;
    pb->mutate();
    *pb;              // OK: pb points to valid memory
    void* q = pb;     // OK: pb points to valid memory
    pb->f();          // undefined behavior: lifetime of *pb has ended
}
— end example]
```

7 Similarly, before the lifetime of an object has started but after the storage which the object will occupy has been allocated or, after the lifetime of an object has ended and before the storage which the object occupied is reused or released, any glvalue that refers to the original object may be used but only in limited ways.

For an object under construction or destruction, see 11.10.5. Otherwise, such a glvalue refers to allocated storage (6.7.5.5.2), and using the properties of the glvalue that do not depend on its value is well-defined. The program has undefined behavior if:

- (7.1) — the glvalue is used to access the object, or
- (7.2) — the glvalue is used to call a non-static member function of the object, or
- (7.3) — the glvalue is bound to a reference to a virtual base class (9.4.4), or
- (7.4) — the glvalue is used as the operand of a dynamic_cast (7.6.1.7) or as the operand of typeid.

8 If, after the lifetime of an object has ended and before the storage which the object occupied is reused or released, a new object is created at the storage location which the original object occupied, a pointer that pointed to the original object, a reference that referred to the original object, or the name of the original object will automatically refer to the new object and, once the lifetime of the new object has started, can be used to manipulate the new object, if the original object is transparently replaceable (see below) by the new object. An object o1 is transparently replaceable by an object o2 if:

- (8.1) — the storage that o2 occupies exactly overlays the storage that o1 occupied, and
- (8.2) — o1 and o2 are of the same type (ignoring the top-level cv-qualifiers), and
- (8.3) — o1 is not a complete const object, and
- (8.4) — neither o1 nor o2 is a potentially-overlapping subobject (6.7.2), and
- (8.5) — either o1 and o2 are both complete objects, or o1 and o2 are direct subobjects of objects p1 and p2, respectively, and p1 is transparently replaceable by p2.

[Example 2:

```
struct C {
    int i;
    void f();
    const C& operator=( const C& );
};

const C& C::operator=( const C& other) {
    if ( this != &other ) {
        this->~C();                 // lifetime of *this ends
        new (this) C(other);        // new object of type C created
        f();                        // well-defined
    }
    return *this;
}

C c1;
C c2;
c1 = c2;                        // well-defined
c1.f();                         // well-defined; c1 refers to a new object of type C
— end example]
```

> [Note 3: If these conditions are not met, a pointer to the new object can be obtained from a pointer that represents the address of its storage by calling std::launder (17.6.5). — end note]

9 If a program ends the lifetime of an object of type T with static (6.7.5.2), thread (6.7.5.3), or automatic (6.7.5.4) storage duration and if T has a non-trivial destructor,34 and another object of the original type does not occupy that same storage location when the implicit destructor call takes place, the behavior of the program is undefined. This is true even if the block is exited with an exception.

[Example 3:

```
class T { };
struct B {
    ~B();
};
```

> 34) That is, an object for which a destructor will be called implicitly—upon exit from the block for an object with automatic storage duration, upon exit from the thread for an object with thread storage duration, or upon exit from the program for an object with static storage duration.

