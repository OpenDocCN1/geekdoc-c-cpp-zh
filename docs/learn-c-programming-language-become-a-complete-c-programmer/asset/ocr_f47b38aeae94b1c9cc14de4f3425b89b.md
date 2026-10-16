few routines.

# 11.5.3 C-Style Cast

From C, C++ inherited the notation (T)e, which performs any conversion that can be expressed as a combination of static_casts, reinterpret_casts, const_casts to make a value of type T from the expression e (§44.2.3). Unfortunately, the C-style cast can also cast from a pointer to a class to a pointer to a private base of that class. Never do that, and hope for a warning from the compiler if you do it by mistake. This C-style cast is far more dangerous than the named conversion operators because the notation is harder to spot in a large program and the kind of conversion intended by the programmer is not explicit. That is, (T)e might be doing a portable conversion between related types, a nonportable conversion between unrelated types, or removing the const modifier from a pointer type. Without knowing the exact types of T and e, you cannot tell.

# Section 11.5.4 Function-Style Cast 303

# 11.5.4 Function-Style Cast

The construction of a value of type T from a value e can be expressed by the functional notation T(e). For example:

```
void f(double d)
{
int i = int(d); // truncated
complex z = complex(d); // makeacomplexfrom d
// ...
}
```

The T(e) construct is sometimes referred to as a function-style cast. Unfortunately, for a built-in type T, T(e) is equivalent to (T)e (§11.5.3). This implies that for many built-in types T(e) is not safe.

```
void f(double d, char * p)
{
int a = int(d); // truncates
int b = int(p); // not portable
// ...
}
```

Even explicit conversion of a longer integer type to a shorter (such as long to char) can result in nonportable implementation-defined behavior.
Prefer T{v} conversions for well-behaved construction and the named casts (e.g., static_cast) for other conversions.

# 11.6 Advice

[1] Prefer prefix ++ over suffix ++; §11.1.4.

[2] Use resource handles to avoid leaks, premature deletion, and double deletion; §11.2.1.