
```
p - q = -14
q - p = 14
```

end example]

If a pointer arithmetic operation overflows the domain of the pointer type, the result is truncated in an implementation-defined fashion, but no exceptions are produced.

## 23.6.8 Pointer comparison

In an unsafe context, the ==, !=, <, >, <=, and >= operators (§12.11) can be applied to values of all pointer types. The pointer comparison operators are:

```
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

Because an implicit conversion exists from any pointer type to the void* type, operands of any pointer type can be compared using these operators. The comparison operators compare the addresses given by the two operands as if they were unsigned integers.

## 23.6.9 The sizeof operator

For certain predefined types (§12.7.13), the sizeof operator yields a constant int value. For all other types, the result of the sizeof operator is implementation-defined and is classified as a value, not a constant.

The order in which members are packed into a struct is unspecified.

For alignment purposes, there may be unnamed padding at the beginning of a struct, within a struct, and at the end of the struct. The contents of the bits used as padding are indeterminate.

When applied to an operand that has struct type, the result is the total number of bytes in a variable of that type, including any padding.

## 23.7 The fixed statement

In an unsafe context, the embedded-statement (§13.1) production permits an additional construct, the fixed statement, which is used to "fix" a moveable variable such that its address remains constant for the duration of the statement.

```
embedded-statement:
  ...
  fixed-statement
fixed-statement:
  fixed ( pointer-type fixed-pointer-declarators ) embedded-statement
fixed-pointer-declarators:
  fixed-pointer-declarator
  fixed-pointer-declarators , fixed-pointer-declarator
fixed-pointer-declarator:
  identifier = fixed-pointer-initializer
fixed-pointer-initializer:
  & variable-reference
  expression
```

Each fixed-pointer-declarator declares a local variable of the given pointer-type and initializes that local variable with the address computed by the corresponding fixed-pointer-initializer. A local variable declared in a fixed statement is accessible in any fixed-pointer-initializers occurring to the right of that variable's declaration, and in the embedded-statement of the fixed statement. A local variable declared by a fixed statement is considered read-only. A compile-time error occurs if the embedded statement attempts to modify this local variable (via assignment or the ++ and -- operators) or pass it as a ref or out parameter.

It is an error to use a captured local variable (§12.16.6.2), value parameter, or parameter array in a fixed-pointer-initializer. A fixed-pointer-initializer can be one of the following:

- The token “&” followed by a variable-reference (§10.5) to a moveable variable (§23.4) of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the given variable, and the variable is guaranteed to remain at a fixed address for the duration of the fixed statement.
- An expression of an array-type with elements of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the first element in the array, and the entire array is guaranteed to remain at a fixed address for the duration of the fixed statement. The behavior of the fixed statement is implementation-defined if the array expression is null or if the array has zero elements.
- An expression of type string, provided the type char* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the first character in the string, and the entire string is guaranteed to remain at a fixed address for the duration of the fixed statement. The behavior of the fixed statement is implementation-defined if the string expression is null.
- A simple-name or member-access that references a fixed-size buffer member of a moveable variable, provided the type of the fixed-size buffer member is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes a pointer to the first element of the fixed-size buffer (§23.8.3), and the fixed-size buffer is guaranteed to remain at a fixed address for the duration of the fixed statement.

For each address computed by a fixed-pointer-initializer the fixed statement ensures that the variable referenced by the address is not subject to relocation or disposal by the garbage collector for the duration of the fixed statement. [Example: If the address computed by a fixed-pointer-initializer references a field of an object or an element of an array instance, the fixed statement guarantees that the containing object instance is not relocated or disposed of during the lifetime of the statement. end example]

It is the programmer’s responsibility to ensure that pointers created by fixed statements do not survive beyond execution of those statements. [Example: When pointers created by fixed statements are passed to external APIs, it is the programmer’s responsibility to ensure that the APIs retain no memory of these pointers. end example]

Fixed objects can cause fragmentation of the heap (because they can’t be moved). For that reason, objects should be fixed only when absolutely necessary and then only for the shortest amount of time possible.

[Example: The example

```csharp
class Test
{
    static int x;
    int y;
    unsafe static void F(int* p) {
        *p = 1;
    }
}
```

```
static void Main() {
    Test t = new Test();
    int[] a = new int[10];
    unsafe {
        fixed (int* p = &x) F(p);
        fixed (int* p = &t.y) F(p);
        fixed (int* p = &a[0]) F(p);
        fixed (int* p = a) F(p);
    }
}
}
```

demonstrates several uses of the fixed statement. The first statement fixes and obtains the address of a static field, the second statement fixes and obtains the address of an instance field, and the third statement fixes and obtains the address of an array element. In each case, it would have been an error to use the regular & operator since the variables are all classified as moveable variables.

The third and fourth fixed statements in the example above produce identical results. In general, for an array instance a, specifying &a[0] in a fixed statement is the same as simply specifying a. Here's another example of the fixed statement, this time using string:

```
class Test
{
    static string name = "xx";
    unsafe static void F(char* p) {
        for (int i = 0; p[i] != '\0'; ++i)
            Console.WriteLine(p[i]);
    }
    static void Main() {
        unsafe {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

end example]

In an unsafe context, array elements of single-dimensional arrays are stored in increasing index order, starting with index 0 and ending with index Length − 1. For multi-dimensional arrays, array elements are stored such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.

Within a fixed statement that obtains a pointer p to an array instance a, the pointer values ranging from p to p + a.Length − 1 represent addresses of the elements in the array. Likewise, the variables ranging from p[0] to p[a.Length − 1] represent the actual array elements. Given the way in which arrays are stored, we can treat an array of any dimension as though it were linear. [Example:

```
using System;
class Test
{
    static void Main() {
        int[,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i) // treat as linear
                    p[i] = i;
            }
        }
    }
}
```
