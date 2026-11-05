```
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

Given an expression P of a pointer type T* and an expression N of type int, uint, long, or ulong, the expressions P + N and P + N compute the pointer value of type T* that results from adding N * sizeof(T) to the address given by P. Likewise, the expression P - N computes the pointer value of type T* that results from subtracting N * sizeof(T) from the address given by P.

Given two expressions, P and Q, of a pointer type T*, the expression P - Q computes the difference between the addresses given by P and Q and then divides that difference by sizeof(T). The type of the result is always long. In effect, P - Q is computed as ((long)(P) - (long)(Q)) / sizeof(T).

For example:

```
using System;
class Test
{
    static void Main() {
        unsafe {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine("p - q = {0}", p - q);
            Console.WriteLine("q - p = {0}", q - p);
        }
    }
}
```

which produces the output:

p - q = -14
q - p = 14

If a pointer arithmetic operation overflows the domain of the pointer type, the result is truncated in an implementation-defined fashion, but no exceptions are produced.

# 18.5.7 Pointer comparison

In an unsafe context, the ==, !=, <, >, <=, and >= operators (§7.10) can be applied to values of all pointer types. The pointer comparison operators are:

```
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

Because an implicit conversion exists from any pointer type to the void* type, operands of any pointer type can be compared using these operators. The comparison operators compare the addresses given by the two operands as if they were unsigned integers.