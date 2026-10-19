is initialized with the value T(v) (7.6.1.4); if a narrowing conversion is required to convert v to U, the program is ill-formed.

```
[Example 7:

```cpp
enum byte : unsigned char { };
byte b { 42 };                         // OK
byte c = { 42 };                       // error
byte d = byte{ 42 };                   // OK; same value as b
byte e { -1 };                         // error

struct A { byte b; };
A a1 = { 42 };                          // error
A a2 = { byte{ 42 } };                 // OK

void f(byte);
f({ 42 });                              // error

enum class Handle : uint32_t { Invalid = 0 };
Handle h { 42 };                       // OK
```
— *end example*]
```

**(3.9)** — Otherwise, if the initializer list has a single element of type E and either T is not a reference type or its referenced type is reference-related to E, the object or reference is initialized from that element (by copy-initialization for copy-list-initialization, or by direct-initialization for direct-list-initialization); if a narrowing conversion (see below) is required to convert the element to T, the program is ill-formed.

```
[Example 8:

```cpp
int x1 {2};                             // OK
int x2 {2.0};                           // error: narrowing
```
— *end example*]
```

**(3.10)** — Otherwise, if T is a reference type, a prvalue is generated. The prvalue initializes its result object by copy-list-initialization. The prvalue is then used to direct-initialize the reference. The type of the temporary is the type referenced by T, unless T is “reference to array of unknown bound of U”, in which case the type of the temporary is the type of x in the declaration `U x[] H`, where H is the initializer list.

> [*Note 3:* As usual, the binding will fail and the program is ill-formed if the reference type is an lvalue reference to a non-const type. — *end note*]

```
[Example 9:

```cpp
struct S {
  S(std::initializer_list<double>);  // #1
  S(const std::string&);              // #2
  // ...
};
const S& r1 = { 1, 2, 3.0 };          // OK: invoke #1
const S& r2 { "Spinach" };            // OK: invoke #2
S& r3 = { 1, 2, 3 };                   // error: initializer is not an lvalue
const int& i1 = { 1 };                 // OK
const int& i2 = { 1.1 };               // error: narrowing
const int (&iar)[2] = { 1, 2 };        // OK: iar is bound to temporary array

struct A { } a;
struct B { explicit B(const A&); };
const B& b2{a};                        // error: cannot copy-list-initialize B temporary from A
```
— *end example*]
```

**(3.11)** — Otherwise, if the initializer list has no elements, the object is value-initialized.

```
[Example 10:

```cpp
int** pp {};                           // initialized to null pointer
```
— *end example*]
```

**(3.12)** — Otherwise, the program is ill-formed.