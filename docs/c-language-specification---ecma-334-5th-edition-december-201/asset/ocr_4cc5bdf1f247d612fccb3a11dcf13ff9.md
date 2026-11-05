A method can return a value of some type, and that type can be a pointer. [Example: When given a pointer to a contiguous sequence of ints, that sequence's element count, and some other int value, the following method returns the address of that value in that sequence, if a match occurs; otherwise it returns null:

```
unsafe static int* Find(int* p, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*p == value)
            return p;
        ++p;
    }
    return null;
}
```

end example

In an unsafe context, several constructs are available for operating on pointers:

+   - The unary * operator may be used to perform pointer indirection (§23.6.2).
+   - The -> operator may be used to access a member of a struct through a pointer (§23.6.3).
+   - The [] operator may be used to index a pointer (§23.6.4).
+   - The unary & operator may be used to obtain the address of a variable (§23.6.5).
+   - The ++ and -- operators may be used to increment and decrement pointers (§23.6.6).
+   - The binary + and - operators may be used to perform pointer arithmetic (§23.6.7).
+   - The ==, !=, <, >, <=, and >= operators may be used to compare pointers (§23.6.8).
+   - The stackalloc operator may be used to allocate memory from the call stack (§23.9).
+   - The fixed statement may be used to temporarily fix a variable so its address can be obtained (§23.7).

# 23.4 Fixed and moveable variables

The address-of operator (§23.6.5) and the fixed statement (§23.7) divide variables into two categories: Fixed variables and moveable variables.

Fixed variables reside in storage locations that are unaffected by operation of the garbage collector. (Examples of fixed variables include local variables, value parameters, and variables created by dereferencing pointers.) On the other hand, moveable variables reside in storage locations that are subject to relocation or disposal by the garbage collector. (Examples of moveable variables include fields in objects and elements of arrays.)

The & operator (§23.6.5) permits the address of a fixed variable to be obtained without restrictions. However, because a moveable variable is subject to relocation or disposal by the garbage collector, the address of a moveable variable can only be obtained using a fixed statement (§23.7), and that address remains valid only for the duration of that fixed statement.

In precise terms, a fixed variable is one of the following:

+   - A variable resulting from a simple-name (§12.7.3) that refers to a local variable, value parameter, or parameter array, unless the variable is captured by an anonymous function (§12.16.6.2).
+   - A variable resulting from a member-access (§12.7.5) of the form V.I, where V is a fixed variable of a struct-type.
+   - A variable resulting from a pointer-indirection-expression (§23.6.2) of the form *P, a pointer-member-access (§23.6.3) of the form P->I, or a pointer-element-access (§23.6.4) of the form P[E].