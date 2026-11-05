```
```csharp
int* values = stackalloc int[20];
int* p = &values[1];
int* q = &values[15];
Console.WriteLine($"p - q = {p - q}");
Console.WriteLine($"q - p = {q - p}");
}
}
```
```

which produces the output:

p - q = -14
q - p = 14

*end example*

If a pointer arithmetic operation overflows the domain of the pointer type, the result is truncated in an implementation-defined fashion, but no exceptions are produced.

# 23.6.8 Pointer comparison

In an unsafe context, the ==, !=, <, >, <=, and >= operators (§12.12) can be applied to values of all pointer types. The pointer comparison operators are:

```
```csharp
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```
```

Because an implicit conversion exists from any pointer type to the void* type, operands of any pointer type can be compared using these operators. The comparison operators compare the addresses given by the two operands as if they were unsigned integers.

# 23.6.9 The sizeof operator

For certain predefined types (§12.8.18), the sizeof operator yields a constant int value. For all other types, the result of the sizeof operator is implementation-defined and is classified as a value, not a constant.

The order in which members are packed into a struct is unspecified.

For alignment purposes, there may be unnamed padding at the beginning of a struct, within a struct, and at the end of the struct. The contents of the bits used as padding are indeterminate.

When applied to an operand that has struct type, the result is the total number of bytes in a variable of that type, including any padding.

# 23.7 The fixed statement

In an unsafe context, the embedded_statement (§13.1) production permits an additional construct, the fixed statement, which is used to "fix" a moveable variable such that its address remains constant for the duration of the statement.

```
```
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
    ;
```
```