```
```cpp
// that is,::count2
// that is,this->m1+::count; that is,::count2+::count // veryodd constructor
```
```

Member initialization is done in declaration order (§17.2.3), so first **m1** is initialized to the value of a global variable **count2**. The value of the global variable is obtained at the point where the constructor for a new **S** object is run, so it can (and in this example does) change. Next, **m2** is initialized by a call to the global **f()**.

It is a bad idea to hide subtle dependencies on global data in member initializers.

# 17.4.5 **static Member Initialization**

A **static** class member is statically allocated rather than part of each object of the class. Generally, the **static** member declaration acts as a declaration for a definition outside the class. For example:

```
```cpp
class Node {
// ...
static int node_count;
};
// declaration
int Node::node_count = 0; // definition
```
```

However, for a few simple special cases, it is possible to initialize a **static** member in the class declaration. The **static** member must be a **const** of an integral or enumeration type, or a **constexpr** of a literal type (§10.4.3), and the initializer must be a *constant-expression*. For example:

```
```cpp
class Curious {
public:
static const int c1 = 7; // OK
static int c2 = 11; // error : not const
const int c3 = 13; // OK, but not static (§17.4.4)
static const int c4 = sqrt(9); // error : in-class initializer not constant
static const float c5 = 7.0; // error : in-class not integral (use constexpr rather than const)
// ...
};
```
```

If (and only if) you use an initialized member in a way that requires it to be stored as an object in memory, the member must be (uniquely) defined somewhere. The initializer may not be repeated: **const int Curious::c1;** // *don't repeat initializer here*  
**const int* p = &Curious::c1;** // *OK: Curious::c1 has been defined*

The main use of member constants is to provide symbolic names for constants needed elsewhere in the class declaration. For example:

```
```cpp
template<class T, int N>
class Fixed { // fixed-size array
public:
static constexpr int max = N;
```
```