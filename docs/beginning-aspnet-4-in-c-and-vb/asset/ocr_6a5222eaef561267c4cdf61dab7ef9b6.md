# Pointer Arithmetic

It is possible to add or subtract integers to and from pointers. However, the compiler is quite clever about how it arranges this. For example, suppose that you have a pointer to an int and you try to add 1 to its value. The compiler will assume that you actually mean you want to look at the memory location following the int, and hence it will increase the value by 4 bytes — the size of an int. If it is a pointer to a double, adding 1 will actually increase the value of the pointer by 8 bytes, the size of a double. Only if the pointer points to a byte or sbyte (1 byte each), will adding 1 to the value of the pointer actually change its value by 1.

You can use the operators +, -, +=, -=, ++, and -- with pointers, with the variable on the right side of these operators being a long or ulong.

> It is not permitted to carry out arithmetic operations on void pointers.

For example, assume these definitions:

```
uint u = 3;
byte b = 8;
double d = 10.0;
uint* pUint = &u;    // size of a uint is 4
byte* pByte = &b;    // size of a byte is 1
double* pDouble = &d; // size of a double is 8
```

Next, assume the addresses to which these pointers point are:

+   - pUint: 1243332
+   - pByte: 1243328
+   - pDouble: 1243320

Then execute this code:

```
++pUint;        // adds (1*4) = 4 bytes to pUint
pByte -= 3;     // subtracts (3*1) = 3 bytes from pByte
double* pDouble2 = pDouble + 4; // pDouble2 = pDouble + 32 bytes (4*8 bytes)
```

The pointers now contain this:

+   - pUint: 1243336
+   - pByte: 1243325
+   - pDouble2: 1243352

> You need to be aware of the previous rule. If successive values of a given type are stored in successive memory locations, pointer addition works very well, allowing you to move pointers between memory locations. If you are dealing with types such as byte or char, though, with sizes not in multiples of 4, successive values will not, by default, be stored in successive memory locations.