```
uint u = 3;
byte b = 8;
double d = 10.0;
uint* pUint= &u;      // size of a uint is 4
byte* pByte = &b;    // size of a byte is 1
double* pDouble = &d; // size of a double is 8
```

Next, assume the addresses to which these pointers point are as follows:

+   - pUint: 1243332
+   - pByte: 1243328
+   - pDouble: 1243320

Then execute this code:

```
++pUint;            // adds (1*4) = 4 bytes to pUint
pByte -= 3;          // subtracts (3*1) = 3 bytes from pByte
double* pDouble2 = pDouble + 4; // pDouble2 = pDouble + 32 bytes
(4*8 bytes)
```

The pointers now contain this:

+   - pUint: 1243336
+   - pByte: 1243325
+   - pDouble2: 1243352

> NOTE The general rule is that adding a number x to a pointer to type T with value P gives the result P + X*(sizeof(T)). If successive values of a given type are stored in successive memory locations, pointer addition works very well, allowing you to move pointers between memory locations. If you are dealing with types such as byte or char, though, with sizes not in multiples of 4, successive values will not, by default, be stored in successive memory locations.

You can also subtract one pointer from another pointer, if both pointers point to the same data type. In this case, the result is a long whose value is given by the difference between the pointer values divided by the size of the type that they represent:

```
double* pD1 = (double*)1243324; // note that it is perfectly valid to
// initialize a pointer like this.
double* pD2 = (double*)1243300;
long L = pD1-pD2;               // gives the result 3
(=24/sizeof(double))
```

# The sizeof Operator

This section has been referring to the size of various data types. If you need to use the size of a type in your code, you can use the sizeof operator, which takes the name of a data type as a parameter and