
## Pointer Arithmetic

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

- pUint: 1243332
- pByte: 1243328
- pDouble: 1243320

Then execute this code:

```
++pUint;        // adds (1*4) = 4 bytes to pUint
pByte -= 3;     // subtracts (3*1) = 3 bytes from pByte
double* pDouble2 = pDouble + 4; // pDouble2 = pDouble + 32 bytes (4*8 bytes)
```

The pointers now contain this:

- pUint: 1243336
- pByte: 1243325
- pDouble2: 1243352

> You need to be aware of the previous rule. If successive values of a given type are stored in successive memory locations, pointer addition works very well, allowing you to move pointers between memory locations. If you are dealing with types such as byte or char, though, with sizes not in multiples of 4, successive values will not, by default, be stored in successive memory locations.

```
(uint)&y2, sizeof(byte), y2);
Console.WriteLine(
    "*Address of z is 0x{0:X}, size is {1}, value is {2}*",
    (uint)&z, sizeof(double), z);
Console.WriteLine(
    "*Address of pX is 0x{0:X}, size is {1}, value is 0x{2:X}*",
    (uint)&pX, sizeof(int*), (uint)pX);
Console.WriteLine(
    "*Address of pY is 0x{0:X}, size is {1}, value is 0x{2:X}*",
    (uint)&pY, sizeof(short*), (uint)pY);
Console.WriteLine(
    "*Address of pZ is 0x{0:X}, size is {1}, value is 0x{2:X}*",
    (uint)&pZ, sizeof(double*), (uint)pZ);

*pX = 20;
Console.WriteLine("After setting *pX, x = {0}", x);
Console.WriteLine("*pX = {0}", *pX);

pZ = (double*)pX;
Console.WriteLine("x treated as a double = {0}", *pZ);

Console.ReadLine();
}
```

This code declares four value variables:

- An int x
- A short y
- A byte y2
- A double z

It also declares pointers to three of these values: pX, pY, and pZ.

Next, you display the values of these variables as well as their sizes and addresses. Note that in taking the address of pX, pY, and pZ, you are effectively looking at a pointer to a pointer — an address of an address of a value. Notice that, in accordance with the usual practice when displaying addresses, you have used the {0:X} format specifier in the Console.WriteLine() commands to ensure that memory addresses are displayed in hexadecimal format.

Finally, you use the pointer pX to change the value of x to 20 and do some pointer casting to see what happens if you try to treat the content of x as if it were a double.

Compiling and running this code results in the following output. This screen output demonstrates the effects of attempting to compile both with and without the /unsafe flag:

```
csc PointerPlayground.cs
Microsoft (R) Visual C# 2010 Compiler version 4.0.21006.1
Copyright (C) Microsoft Corporation. All rights reserved.

PointerPlayground.cs(7,26): error CS0227: Unsafe code may only appear if
    compiling with /unsafe

csc /unsafe PointerPlayground.cs
Microsoft (R) Visual C# 2010 Compiler version 4.0.21006.1
Copyright (C) Microsoft Corporation. All rights reserved.

PointerPlayground
```

Similarly, to store 20 double data items, you write this:

```
double* pDoubles = stackalloc double[20];
```

Although this line of code specifies the number of variables to store as a constant, this can equally be a quantity evaluated at runtime. So, you can write the previous example like this:

```
int size;
size = 20; // or some other value calculated at run-time
double* pDoubles = stackalloc double[size];
```

You can see from these code snippets that the syntax of stackalloc is slightly unusual. It is followed immediately by the name of the data type you want to store (and this must be a value type) and then by the number of items you need space for in square brackets. The number of bytes allocated will be this number multiplied by sizeof(data type). The use of square brackets in the preceding code sample suggests an array, which is not too surprising. If you have allocated space for 20 doubles, then what you have is an array of 20 doubles. The simplest type of array that you can have is a block of memory that stores one element after another (see Figure 13-6).

![](img/d7d2ffa0a76feaab821930e95daace93_391_0.png)

## FIGURE 13-6

This diagram also shows the pointer returned by stackalloc, which is always a pointer to the allocated data type that points to the top of the newly allocated memory block. To use the memory block, you simply dereference the returned pointer. For example, to allocate space for 20 doubles and then set the first element (element 0 of the array) to the value 3.0, write this:

```
double* pDoubles = stackalloc double [20];
*pDoubles = 3.0;
```

To access the next element of the array, you use pointer arithmetic. As described earlier, if you add 1 to a pointer, its value will be increased by the size of whatever data type it points to. In this case, this will be just enough to take you to the next free memory location in the block that you have allocated. So, you can set the second element of the array (element number 1) to the value 8.4 like this:

```
double* pDoubles = stackalloc double [20];
*pDoubles = 3.0;
*(pDoubles+1) = 8.4;
```

By the same reasoning, you can access the element with index x of the array with the expression *(pDoubles+x).

Effectively, you have a means by which you can access elements of your array, but for general-purpose use, this syntax is too complex. Fortunately, C# defines an alternative syntax using square brackets when they are applied to pointers; C# gives a very precise meaning to square brackets when they are applied to pointers; if the variable p is any pointer type and x is an integer, then the expression p[x] is always interpreted by the compiler as meaning *(p+x). This is true for all pointers, not only those initialized using stackalloc. With this shorthand notation, you now have a very convenient syntax for accessing your array. In fact, it means that you have exactly the same syntax for accessing 1-dimensional stack-based arrays as you do for accessing heap-based arrays that are represented by the System.Array class:

```
double* pDoubles = stackalloc double [20];
pDoubles[0] = 3.0; // pDoubles[0] is the same as *pDoubles
pDoubles[1] = 8.4; // pDoubles[1] is the same as *(pDoubles+1)
```

> This idea of applying array syntax to pointers is not new. It has been a fundamental part of both the C and the C++ languages ever since those languages were invented. Indeed, C++ developers will recognize the stack-based arrays they can obtain using stackalloc as being essentially identical to classic stack-based C and C++ arrays. This syntax and the way it links pointers and arrays is one reason why the C language became popular in the 1970s, and the main reason why the use of pointers became such a popular programming technique in C and C++.

Although your high-performance array can be accessed in the same way as a normal C# array, a word of caution is in order. The following code in C# raises an exception:

```
double[] myDoubleArray = new double [20];
myDoubleArray[50] = 3.0;
```

The exception occurs because you are trying to access an array using an index that is out of bounds; the index is 50, whereas the maximum allowed value is 19. However, if you declare the equivalent array using stackalloc, there is no object wrapped around the array that can perform bounds checking. Hence, the following code will not raise an exception:

```
double* pDoubles = stackalloc double [20];
pDoubles [50] = 3.0;
```

In this code, you allocate enough memory to hold 20 doubles. Then you set sizeof(double) memory locations, starting at the location given by the start of this memory + 50*sizeof(double) to hold the double value 3.0. Unfortunately, that memory location is way outside the area of memory that you have allocated for the doubles. There is no knowing what data might be stored at that address. At best, you may have used some currently unused memory, but it is equally possible that you may have just overwritten some locations in the stack that were being used to store other variables or even the return address from the method currently being executed. Once again, you see that the high performance to be gained from pointers comes at a cost; you need to be certain you know what you are doing, or you will get some very strange runtime bugs.

## QuickArray Example

Our discussion of pointers ends with a stackalloc example called QuickArray. In this example, the program simply asks users how many elements they want to be allocated for an array. The code then uses stackalloc to allocate an array of longs that size. The elements of this array are populated with the squares of the integers starting with 0 and the results are displayed on the console:

```
using System;

namespace QuickArray
{
    internal class Program
    {
        private static unsafe void Main()
        {
            Console.Write("How big an array do you want? \n> ");
            string userInput = Console.ReadLine();
            uint size = uint.Parse(userInput);

            long* pArray = stackalloc long[(int) size];
            for (int i = 0; i < size; i++)
            {
                pArray[i] = i*i;
            }

            for (int i = 0; i < size; i++)
```
