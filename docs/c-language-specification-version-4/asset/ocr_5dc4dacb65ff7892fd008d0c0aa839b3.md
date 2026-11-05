The void* type represents a pointer to an unknown type. Because the referent type is unknown, the indirection operator cannot be applied to a pointer of type void*, nor can any arithmetic be performed on such a pointer. However, a pointer of type void* can be cast to any other pointer type (and vice versa).

Pointer types are a separate category of types. Unlike reference types and value types, pointer types do not inherit from object and no conversions exist between pointer types and object. In particular, boxing and unboxing (§4.3) are not supported for pointers. However, conversions are permitted between different pointer types and between pointer types and the integral types. This is described in §18.4.

A pointer-type cannot be used as a type argument (§4.4), and type inference (§7.5.2) fails on generic method calls that would have inferred a type argument to a pointer type.

A pointer-type may be used as the type of a volatile field (§10.5.3).

Although pointers can be passed as ref or out parameters, doing so can cause undefined behavior, since the pointer may well be set to point to a local variable which no longer exists when the called method returns, or the fixed object to which it used to point, is no longer fixed. For example:

```
using System;
class Test
{
    static int value = 20;
    unsafe static void F(out int* pi1, ref int* pi2) {
        int i = 10;
        pi1 = &i;
        fixed (int* pj = &value) {
            // ...
            pi2 = pj;
        }
    }

    static void Main() {
        int i = 10;
        unsafe {
            int* px1;
            int* px2 = &i;
            F(out px1, ref px2);
            Console.WriteLine("{0}, *px2 = {1}",
                *px1, *px2);  // undefined behavior
        }
    }
}
```

A method can return a value of some type, and that type can be a pointer. For example, when given a pointer to a contiguous sequence of ints, that sequence's element count, and some other int value, the following method returns the address of that value in that sequence, if a match occurs; otherwise it returns null:

```
unsafe static int* Find(int* pi, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*pi == value)
            return pi;
        ++pi;
    }
    return null;
}
```

In an unsafe context, several constructs are available for operating on pointers:

+   - The * operator may be used to perform pointer indirection (§18.5.1).
+   - The -> operator may be used to access a member of a struct through a pointer (§18.5.2).