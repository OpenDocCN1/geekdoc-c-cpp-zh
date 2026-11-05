
## 18.5.4 The Address-of Operator

An addressof-expression consists of an ampersand (&) followed by a unary-expression.

addressof-expression:
    & unary-expression

Given an expression E that is of a type T and is classified as a fixed variable (§18.3), the construct &E computes the address of the variable given by E. The type of the result is T* and is classified as a value. A compile-time error occurs if E is not classified as a variable, if E is classified as a read-only local variable, or if E denotes a moveable variable. In the last case, a fixed statement (§18.6) can be used to temporarily "fix" the variable before obtaining its address. As stated in §7.6.4, outside an instance constructor or static constructor for a struct or class that defines a readonly field, that field is considered a value, not a variable. As such, its address cannot be taken. Similarly, the address of a constant cannot be taken.

The & operator does not require its argument to be definitely assigned, but following an & operation, the variable to which the operator is applied is considered definitely assigned in the execution path in which the operation occurs. It is the responsibility of the programmer to ensure that correct initialization of the variable actually does take place in this situation.

In the example

```
using System;
class Test
{
    static void Main()
    {
        int i;
        unsafe
        {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```

i is considered definitely assigned following the &i operation used to initialize p. The assignment to *p in effect initializes i, but the inclusion of this initialization is the responsibility of the programmer, and no compile-time error would occur if the assignment was removed.

The rules of definite assignment for the & operator exist such that redundant initialization of local variables can be avoided. For example, many external APIs take a pointer to a structure that is filled in by the API. Calls to such APIs typically pass the address of a local struct variable, and without the rule, redundant initialization of the struct variable would be required.

## 18.5.5 Pointer Increment and Decrement

In an unsafe context, the ++ and -- operators (§7.6.9 and §7.7.5) can be applied to pointer variables of all types except void*. Thus, for every pointer type T*, the following operators are implicitly defined:

```
T* operator ++(T* x);
T* operator --(T* x);
```

The operators produce the same results as x + 1 and x - 1, respectively (§18.5.6). In other words, for a pointer variable of type T*, the ++ operator adds sizeof(T) to the address contained in the variable, and the -- operator subtracts sizeof(T) from the address contained in the variable.

If a pointer increment or decrement operation overflows the domain of the pointer type, the result is implementation-defined, but no exceptions are produced.

## 18.5.6 Pointer Arithmetic

In an unsafe context, the + and - operators (§7.8.4 and §7.8.5) can be applied to values of all pointer types except void*. Thus, for every pointer type T*, the following operators are implicitly defined:

```
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);
T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);
T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);
long operator -(T* x, T* y);
```

Given an expression P of a pointer type T* and an expression N of type int, uint, long, or ulong, the expressions P + N and N + P compute the pointer value of type T* that results from adding N * sizeof(T) to the address given by P. Likewise, the expression P - N computes the pointer value of type T* that results from subtracting N * sizeof(T) from the address given by P.

Given two expressions, P and Q, of a pointer type T*, the expression P - Q computes the difference between the addresses given by P and Q and then divides that difference by sizeof(T). The type of the result is always long. In effect, P - Q is computed as ((long)(P) - (long)(Q)) / sizeof(T).

For example,

```
using System;
class Test
{
    static void Main()
    {
        unsafe
        {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine("p - q = {0}", p - q);
            Console.WriteLine("q - p = {0}", q - p);
        }
    }
}
```

produces the following output:

p - q = -14
q - p = 14

If a pointer arithmetic operation overflows the domain of the pointer type, the result is truncated in an implementation-defined fashion, but no exceptions are produced.

## 18.5.7 Pointer Comparison

In an unsafe context, the ==, !=, <, <=, >, and >= operators (§7.10) can be applied to values of all pointer types. The pointer comparison operators are:

```
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

Because an implicit conversion exists from any pointer type to the void* type, operands of any pointer can be compared using these operators. The comparison operators compare the addresses given by the two operands as if they were unsigned integers.

## 18.5.8 The sizeof Operator

The sizeof operator returns the number of bytes occupied by a variable of a given type.
The type specified as an operand to sizeof must be an unmanaged-type (§18.2).

```
sizeof-expression:
    sizeof ( unmanaged-type )
```

The result of the sizeof operator is a value of type int. For certain predefined types, the sizeof operator yields a constant value as shown in the table below.

| Expression | Result |
|---|---|
| sizeof(sbyte) | 1 |
| sizeof(byte) | 1 |
| sizeof(short) | 2 |
| sizeof(ushort) | 2 |
| sizeof(int) | 4 |
| sizeof(uint) | 4 |
| sizeof(long) | 8 |
| sizeof(ulong) | 8 |
| sizeof(char) | 2 |
| sizeof(float) | 4 |
| sizeof(double) | 8 |
| sizeof(bool) | 1 |

For all other types, the result of the sizeof operator is implementation-defined and is classified as a value, not a constant.

The order in which members are packed into a struct is unspecified.

For alignment purposes, there may be unnamed padding at the beginning of a struct, within a struct, and at the end of the struct. The contents of the bits used as padding are indeterminate.

When applied to an operand that has struct type, the result is the total number of bytes in a variable of that type, including any padding.

## 18.6 The fixed Statement

In an unsafe context, the embedded-statement (§8) production permits an additional construct, the fixed statement, which is used to “fix” a movable variable such that its address remains constant for the duration of the statement.

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

Each fixed-pointer-declarator declares a local variable of the given pointer-type and initializes that local variable with the address computed by the corresponding fixed-pointer-initializer. A local variable declared in a fixed statement is accessible in any fixed-pointer-initializers occurring to the right of that variable’s declaration, and in the embedded-statement of the fixed statement. A local variable declared by a fixed statement is considered read-only. A compile-time error occurs if the embedded statement attempts to modify this local variable (via assignment or the ++ and -- operators) or pass it as a ref or out parameter.

A fixed-pointer-initializer can be one of the following:

- The token “&” followed by a variable-reference (§5.3.3) to a movable variable (§18.3) of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the given variable, and the variable is guaranteed to remain at a fixed address for the duration of the fixed statement.
- An expression of an array-type with elements of an unmanaged type T, provided the type T* is implicitly convertible to the pointer type given in the fixed statement. In this case, the initializer computes the address of the first element in the array, and the entire array is guaranteed to remain at a fixed address for the duration of the fixed statement. The
