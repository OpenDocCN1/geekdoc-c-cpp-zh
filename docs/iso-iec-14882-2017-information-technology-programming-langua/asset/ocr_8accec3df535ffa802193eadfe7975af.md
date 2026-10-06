# ISO/IEC 14882:2017(E)

(1.7) If T is a class, it has a public assignment operator whose signature is either T& T::operator=(const T&) or T& T::operator=(T)

(1.8) If T is a class, its assignment operator, copy and default constructors, and destructor shall correspond to each in the following line:

+   - (1.8.1) Initialization of raw storage using the copy constructor on the value of T(), however obtained, is semantically equivalent to value-initialization of the raw storage

+   - (1.8.2) Initialization of raw storage using the default constructor, followed by assignment, is semantically equivalent to initialization of raw storage using the copy constructor.

+   - (1.8.3) Destruction of an object, followed by initialization of raw storage using the copy constructor, is semantically equivalent to the original object.

> [Note: This rule, in places, is that there shall not be any differences in the semantics of initialization versus assignment. This gives an implementation considerable clarity in how arrays are initialized.

> [Example: An implementation is allowed to initialize a varray by allocating storage using the new operator (which implies a call to the default constructor for each element) and then assigning each element its value. Or implementation can allocate raw storage and use the copy constructor to initialize each. — end example]

If the difference between initialization and assignment is important for a class, or if it fails to satisfy any of the other conditions listed above, the programmer should use vector (26.3.11) instead of varray for that class.

(1.9) If it is a operation on T does not overload the exception operator.

2 In addition, many member and related functions of varray<T> can be successfully instantiated and exhibit well-defined behavior if only if T satisfies additional requirements for each member or related function.

> [Example: It is valid to instantiate varray<complex>, but operator() will not be successfully instantiated for varray<complex> operands, since complex does not have any ordering operators. — end example]

# 29.4 The floating-point environment [cfenv]

# 29.4.1 Header <cfenv> synopsis [cfenv.syn]

```
#define FE_ALL_EXCEPT see below
#define FE_DIVZERO see below
#define FE_INVALID see below
#define FE_INVALID see below
#define FE_OVERFLOW see below
#define FE_UNDERFLOW see below

#define FE_DOWNWARD see below
#define FE_TONAREST see below
#define FE_TOWARDZERO see below
#define FE_UPWARD see below

#define FE_DFL_ENV see below
```

```
namespace std {
// types
using fenv_t = object type;
using fxecept_t = integer type;
```