```
fixed-pointer-declarator:
    identifier = fixed-pointer-initializer

fixed-pointer-initializer:
    & variable-reference
    expression
```

Each fixed-pointer-declarator declares a local variable of the given pointer-type and initializes that local variable with the address computed by the corresponding fixed-pointer-initializer. A local variable declared in a fixed statement is accessible in any fixed-pointer-initializers occurring to the right of that variable's declaration, and in the embedded-statement of the fixed statement. A local variable declared by a fixed statement is considered read-only. A compile-time error occurs if the embedded statement attempts to modify this local variable (via assignment or the ++ and -- operators) or pass it as a ref or out parameter.

A fixed-pointer-initializer can be one of the following:

+   - The token "&" followed by a variable-reference (§5.3.3) to a moveable variable (§18.3) of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the given variable, and the variable is guaranteed to remain at a fixed address for the duration of the fixed statement.
+   - An expression of an array-type with elements of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the first element in the array, and the entire array is guaranteed to remain at a fixed address for the duration of the fixed statement. The behavior of the fixed statement is implementation-defined if the array expression is null or if the array has zero elements.
+   - An expression of type string, provided the type char* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the first character in the string, and the entire string is guaranteed to remain at a fixed address for the duration of the fixed statement. The behavior of the fixed statement is implementation-defined if the string expression is null.
+   - A simple-name or member-access that references a fixed size buffer member is a moveable variable, provided the type of the fixed size buffer member is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes a pointer to the first element of the fixed size buffer (§18.7.2), and the fixed size buffer is guaranteed to remain at a fixed address for the duration of the fixed statement.

For each address computed by a fixed-pointer-initializer the fixed statement ensures that the variable referenced by the address is not subject to relocation or disposal by the garbage collector for the duration of the fixed statement. For example, if the address computed by a fixed-pointer-initializer references a field of an object or an element of an array instance, the fixed statement guarantees that the containing object instance is not relocated or disposed of during the lifetime of the statement.

It is the programmer's responsibility to ensure that pointers created by fixed statements do not survive beyond execution of those statements. For example, when pointers created by fixed statements are passed to external APIs, it is the programmer's responsibility to ensure that the APIs retain no memory of these pointers.

Fixed objects may cause fragmentation of the heap (because they can't be moved). For that reason, objects should be fixed only when absolutely necessary and then only for the shortest amount of time possible.

The example

```
class Test
{
    static int x;
    int y;
```