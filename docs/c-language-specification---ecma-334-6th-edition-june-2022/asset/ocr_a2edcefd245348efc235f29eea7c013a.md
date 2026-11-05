| | |
|---|---|
| byte* | Pointer to byte |
| char* | Pointer to char |
| int** | Pointer to pointer to int |
| int*[] | Single-dimensional array of pointers to int |
| void* | Pointer to unknown type |

*end example*

For a given implementation, all pointer types shall have the same size and representation.

*Note*: Unlike C and C++, when multiple pointers are declared in the same declaration, in C# the * is written along with the underlying type only, not as a prefix punctuator on each pointer name. For example:

```
```csharp
int* pi, pj; // NOT as int *pi, *pj;
```
```

*end note*

The value of a pointer having type `T*` represents the address of a variable of type `T`. The pointer indirection operator `*` (§22.6.2) can be used to access this variable.

*Example*: Given a variable `P` of type `int*`, the expression `*P` denotes the `int` variable found at the address contained in `P`. *end example*

Like an object reference, a pointer may be `null`. Applying the indirection operator to a `null`-valued pointer results in implementation-defined behavior (§22.6.2). A pointer with value `null` is represented by all-bits-zero.

The `void*` type represents a pointer to an unknown type. Because the referent type is unknown, the indirection operator cannot be applied to a pointer of type `void*`, nor can any arithmetic be performed on such a pointer. However, a pointer of type `void*` can be cast to any other pointer type (and vice versa) and compared to values of other pointer types (§22.6.8).

Pointer types are a separate category of types. Unlike reference types and value types, pointer types do not inherit from `object` and no conversions exist between pointer types and `object`. In particular, boxing and unboxing (§8.3.12) are not supported for pointers. However, conversions are permitted between different pointer types and between pointer types and the integral types. This is described in §22.5.

A `pointer_type` cannot be used as a type argument (§8.4), and type inference (§11.6.3) fails on generic method calls that would have inferred a type argument to be a pointer type.

A `pointer_type` cannot be used as a type of a subexpression of a dynamically bound operation (§11.3.3).

A `pointer_type` may be used as the type of a volatile field (§14.5.4).

*Note*: Although pointers can be passed as `ref` or `out` parameters, doing so can cause undefined behavior, since the pointer might well be set to point to a local variable that no longer exists when the called method returns, or the fixed object to which it used to point, is no longer fixed. For example:

```
```csharp
using System;

class Test
{
    static int value = 20;
```
```