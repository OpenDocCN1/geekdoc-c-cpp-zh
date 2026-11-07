
```text
The number of bytes in the array is 160
The number of bytes returned by getSize is 4
```

**Fig. 8.14** | *sizeof* operator when applied to an array name returns the number of bytes in the array. *(Part 2 of 2.)*

The number of elements in an array also can be determined using the results of two `sizeof` operations. For example, consider the following array declaration:

```cpp
double realArray[ 22 ];
```

If variables of data type `double` are stored in eight bytes of memory, array `realArray` contains a total of 176 bytes. To determine the number of elements in the array, the following expression (which is evaluated at compile time) can be used:

```cpp
sizeof realArray / sizeof( realArray[ 0 ] )
```

The expression determines the number of bytes in array `realArray` (176) and divides that value by the number of bytes used in memory to store the array’s first element (typically 8 for a double value)—the result is the number of elements in `realArray` (22).

## Determining the Sizes of the Fundamental Types, an Array and a Pointer

Figure 8.15 uses `sizeof` to calculate the number of bytes used to store most of the standard data types. The output shows that the types double and long double have the same size. Types may have different sizes based on the platform running the program. On another system, for example, double and long double may be of different sizes.

```cpp
// Fig. 8.15: fig08_15.cpp
// Demonstrating the sizeof operator.
#include <iostream>
using namespace std;

int main()
{
   char c; // variable of type char
   short s; // variable of type short
   int i; // variable of type int
   long l; // variable of type long
   float f; // variable of type float
   double d; // variable of type double
   long double ld; // variable of type long double
   int array[ 20 ]; // array of int
   int *ptr = array; // variable of type int *

   cout << "sizeof c = " << sizeof c
      << "\nsizeof(char) = " << sizeof( char )
      << "\nsizeof s = " << sizeof s
      << "\nsizeof(short) = " << sizeof( short )
      << "\nsizeof i = " << sizeof i
```

**Fig. 8.15** | *sizeof* operator used to determine standard data type sizes. *(Part 1 of 2.)*

```c
int *vPtr = v;
int *vPtr = &v[ 0 ];
```

### Portability Tip 8.2

Most computers today have two-byte or four-byte integers. Some of the newer machines use eight-byte integers. Because the results of pointer arithmetic depend on the size of the objects a pointer points to, pointer arithmetic is machine dependent.

![](img/bfd978e7e9b192bab46ec2a89e481263_383_0.png)

**Fig. 8.16**  |  Array v and a pointer variable int *vPtr that points to v.

In conventional arithmetic, the addition 3000 + 2 yields the value 3002. This is normally not the case with pointer arithmetic. When an integer is added to, or subtracted from, a pointer, the pointer is not simply incremented or decremented by that integer, but by that integer times the size of the object to which the pointer refers. The number of bytes depends on the object's data type. For example, the statement

```c
vPtr += 2;
```

would produce 3008 (from the calculation 3000 + 2 * 4), assuming that an int is stored in four bytes of memory. In the array v, vPtr would now point to v[2] (Fig. 8.17). If an integer is stored in two bytes of memory, the preceding calculation would result in memory location 3004 (3000 + 2 * 2). If the array elements were of a different data type, the preceding statement would increment the pointer by twice the number of bytes it takes to store an object of that data type.

![](img/bfd978e7e9b192bab46ec2a89e481263_383_1.png)

**Fig. 8.17**  |  Pointer vPtr after pointer arithmetic.

If vPtr had been incremented to 3016, which points to v[4], the statement

```c
vPtr -= 4;
```

would set vPtr back to 3000—the beginning of the array. If a pointer is being incremented or decremented by one, the increment (++) and decrement (--) operators can be used. Each of the statements

```c
++vPtr;
vPtr++;
```

increments the pointer to point to the *next* element of the array. Each of the statements

```c
--vPtr;
vPtr--;
```

decrements the pointer to point to the *previous* element of the array.

Pointer variables pointing to the *same* array may be subtracted from one another. For example, if vPtr contains the address 3000 and v2Ptr contains the address 3008, the statement

```c
x = v2Ptr - vPtr;
```

would assign to x the *number of array elements* from vPtr to v2Ptr—in this case, 2. Pointer arithmetic is meaningless unless performed on a pointer that points to an array. We cannot assume that two variables of the same type are stored contiguously in memory unless they’re adjacent elements of an array.

> **Common Programming Error 8.8**
> 
> *Subtracting or comparing two pointers that do not refer to elements of the same array is a logic error.*

A pointer can be assigned to another pointer if both pointers are of the *same* type. Otherwise, a cast operator (normally a reinterpret_cast; discussed in Section 17.7) must be used to convert the value of the pointer on the right of the assignment to the pointer type on the left of the assignment. The exception to this rule is the pointer to void (i.e., void *), which is a generic pointer capable of representing any pointer type. All pointer types can be assigned to a pointer of type void * without casting. However, a pointer of type void * **cannot** be assigned directly to a pointer of another type—the pointer of type void * must first be cast to the proper pointer type.

> **Software Engineering Observation 8.5**
> 
> *Nonconstant pointer arguments can be passed to constant pointer parameters.*

A void * pointer *cannot* be dereferenced. For example, the compiler “knows” that a pointer to int refers to four bytes of memory on a machine with four-byte integers, but a pointer to void simply contains a memory address for an unknown data type—the precise number of bytes to which the pointer refers and the type of the data are *not* known by the compiler. The compiler must know the data type to determine the number of bytes to be dereferenced for a particular pointer—for a pointer to void, this number of bytes cannot be determined.

The array name (which is implicitly const) can be treated as a pointer and used in pointer arithmetic. For example, the expression

```c
*( b + 3 )
```

also refers to the array element b[3]. In general, all subscripted array expressions can be written with a pointer and an offset. In this case, pointer/offset notation was used with the name of the array as a pointer. The preceding expression does not modify the array name in any way; b still points to the first element in the array.

Pointers can be subscripted exactly as arrays can. For example, the expression

```c
bPtr[ 1 ]
```

refers to the array element b[1]; this expression uses pointer/subscript notation.

Remember that an array name is a constant pointer; it always points to the beginning of the array. Thus, the expression

```c
b += 3
```

causes a compilation error, because it attempts to modify the value of the array name (a constant) with pointer arithmetic.

![](img/bfd978e7e9b192bab46ec2a89e481263_386_0.png)

> **Common Programming Error 8.11**
> 
> *Although array names are pointers to the beginning of the array, array names cannot be modified in arithmetic expressions, because array names are constant pointers.*

![](img/bfd978e7e9b192bab46ec2a89e481263_386_1.png)

> **Good Programming Practice 8.2**
> 
> *For clarity, use array notation instead of pointer notation when manipulating arrays.*

Figure 8.18 uses the four notations discussed in this section for referring to array elements—array subscript notation, pointer/offset notation with the array name as a pointer, pointer subscript notation and pointer/offset notation with a pointer—to accomplish the same task, namely printing the four elements of the integer array b.

```cpp
// Fig. 8.18: fig08_18.cpp
// Using subscripting and pointer notations with arrays.
#include <iostream>
using namespace std;

int main()
{
    int b[] = { 10, 20, 30, 40 }; // create 4-element array b
    int *bPtr = b; // set bPtr to point to array b

    // output array b using array subscript notation
    cout << "Array b printed with:\n\nArray subscript notation\n";

    for ( int i = 0; i < 4; ++i )
        cout << "b[" << i << "] = " << b[ i ] << '\n';
```

**Fig. 8.18** | Referencing array elements with the array name and with pointers. (Part 1 of 2.)
