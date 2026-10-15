
## Portability Tip 8.2

> The number of bytes used to store a particular data type may vary among systems. When writing programs that depend on data type sizes, and that will run on several computer systems, use sizeof to determine the number of bytes used to store the data types.

Operator sizeof can be applied to any expression or type name. When sizeof is applied to a variable name (which is not an array name) or other expression, the number of bytes used to store the specific type of the expression’s value is returned. Note that the parentheses used with sizeof are required only if a type name (e.g., int) is supplied as its operand. The parentheses used with sizeof are not required when sizeof’s operand is an expression. Remember that sizeof is an operator, not a function, and that it has its effect at compile time, not execution time.

## Common Programming Error 8.8

> Omitting the parentheses in a sizeof operation when the operand is a type name is a compilation error.

## Performance Tip 8.2

> Because sizeof is a compile-time unary operator, not an execution-time operator, using sizeof does not negatively impact execution performance.

## Error-Prevention Tip 8.3

> To avoid errors associated with omitting the parentheses around the operand of operator sizeof, many programmers include parentheses around every sizeof operand.

## 8.8 Pointer Expressions and Pointer Arithmetic

Pointers are valid operands in arithmetic expressions, assignment expressions and comparison expressions. However, not all the operators normally used in these expressions are valid with pointer variables. This section describes the operators that can have pointers as operands and how these operators are used with pointers.

Several arithmetic operations may be performed on pointers. A pointer may be incremented (++) or decremented (--), an integer may be added to a pointer (+ or +=), an integer may be subtracted from a pointer (- or -=) or one pointer may be subtracted from another of the same type.

Assume that array int v[5] has been declared and that its first element is at memory location 3000. Assume that pointer vPtr has been initialized to point to v[0] (i.e., the value of vPtr is 3000). Figure 8.18 diagrams this situation for a machine with four-byte integers. Note that vPtr can be initialized to point to array v with either of the following statements (because the name of an array is equivalent to the address of its first element):

```
int *vPtr = v;
int *vPtr = &v[0];
```

## Portability Tip 8.3

> Most computers today have two-byte or four-byte integers. Some of the newer machines use eight-byte integers. Because the results of pointer arithmetic depend on the size of the objects a pointer points to, pointer arithmetic is machine dependent.

increments the pointer to point to the next element of the array. Each of the statements

```
--vPtr;
vPtr--;
```

decrements the pointer to point to the previous element of the array.

Pointer variables pointing to the same array may be subtracted from one another. For example, if vPtr contains the address 3000 and v2Ptr contains the address 3008, the statement

```
x = v2Ptr - vPtr;
```

would assign to x the number of array elements from vPtr to v2Ptr—in this case, 2. Pointer arithmetic is meaningless unless performed on a pointer that points to an array. We cannot assume that two variables of the same type are stored contiguously in memory unless they are adjacent elements of an array.

## Common Programming Error 8.9

Using pointer arithmetic on a pointer that does not refer to an array of values is a logic error.

## Common Programming Error 8.10

Subtracting or comparing two pointers that do not refer to elements of the same array is a logic error.

## Common Programming Error 8.11

Using pointer arithmetic to increment or decrement a pointer such that the pointer refers to an element outside the bounds of the array is normally a logic error.

A pointer can be assigned to another pointer if both pointers are of the same type. Otherwise, a cast operator must be used to convert the value of the pointer on the right of the assignment to the pointer type on the left of the assignment. The exception to this rule is the pointer to void (i.e., void *), which is a generic pointer capable of representing any pointer type. All pointer types can be assigned to a pointer of type void * without casting. However, a pointer of type void * cannot be assigned directly to a pointer of another type—the pointer of type void * must first be cast to the proper pointer type.

## Software Engineering Observation 8.5

Nonconstant pointer arguments can be passed to constant pointer parameters. This is helpful when the body of a program uses a nonconstant pointer to access data, but does not want that data to be modified by a function called in the body of the program.

A void * pointer cannot be dereferenced. For example, the compiler “knows” that a pointer to int refers to four bytes of memory on a machine with four-byte integers, but a pointer to void simply contains a memory address for an unknown data type—the precise number of bytes to which the pointer refers and the type of the data are not known by the compiler. The compiler must know the data type to determine the number of bytes to be dereferenced for a particular pointer—for a pointer to void, this number of bytes cannot be determined from the type.

The array name (which is implicitly const) can be treated as a pointer and used in pointer arithmetic. For example, the expression

```
*( b + 3 )
```

also refers to the array element `b[3]`. In general, all subscripted array expressions can be written with a pointer and an offset. In this case, pointer/offset notation was used with the name of the array as a pointer. Note that the preceding expression does not modify the array name in any way; b still points to the first element in the array.

Pointers can be subscripted exactly as arrays can. For example, the expression

```
bPtr[1]
```

refers to the array element `b[1]`; this expression uses **pointer/subscript notation**. Remember that an array name is a constant pointer; it always points to the beginning of the array. Thus, the expression

```
b += 3
```

causes a compilation error, because it attempts to modify the value of the array name (a constant) with pointer arithmetic.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_358_0.png)

## Common Programming Error 8.14

> Although array names are pointers to the beginning of the array and pointers can be modified in arithmetic expressions, array names cannot be modified in arithmetic expressions, because array names are constant pointers.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_358_1.png)

## Good Programming Practice 8.2

> For clarity, use array notation instead of pointer notation when manipulating arrays.

Figure 8.20 uses the four notations discussed in this section for referring to array elements—array subscript notation, pointer/offset notation with the array name as a pointer, pointer subscript notation and pointer/offset notation with a pointer—to accomplish the same task, namely printing the four elements of the integer array b.

```
// Fig. 8.20: fig08_20.cpp
// Using subscripting and pointer notations with arrays.
#include <iostream>
using std::cout;
using std::endl;

int main()
{
   int b[] = { 10, 20, 30, 40 }; // create 4-element array b
   int *bPtr = b; // set bPtr to point to array b

   // output array b using array subscript notation
   cout << "Array b printed with:\n\nArray subscript notation\n";
```

**Fig. 8.20** | Referencing array elements with the array name and with pointers. (Part 1 of 2.)

```
14
15    for ( int i = 0; i < 4; i++ )
16        cout << "b[" << i << "] = " << b[ i ] << '\n';
17
18    // output array b using the array name and pointer/offset notation
19    cout << "\nPointer/offset notation where "
20        << "the pointer is the array name\n";
21
22    for ( int offset1 = 0; offset1 < 4; offset1++ )
23        cout << "*(b + " << offset1 << ") = " << *( b + offset1 ) << '\n';
24
25    // output array b using bPtr and array subscript notation
26    cout << "\nPointer subscript notation\n";
27
28    for ( int j = 0; j < 4; j++ )
29        cout << "bPtr[" << j << "] = " << bPtr[ j ] << '\n';
30
31    cout << "\nPointer/offset notation\n";
32
33    // output array b using bPtr and pointer/offset notation
34    for ( int offset2 = 0; offset2 < 4; offset2++ )
35        cout << "*(bPtr + " << offset2 << ") = "
36            << *( bPtr + offset2 ) << '\n';
37
38    return 0; // indicates successful termination
39 } // end main
```

Array b printed with:

Array subscript notation
b[0] = 10
b[1] = 20
b[2] = 30
b[3] = 40

Pointer/offset notation where the pointer is the array name
*(b + 0) = 10
*(b + 1) = 20
*(b + 2) = 30
*(b + 3) = 40

Pointer subscript notation
bPtr[0] = 10
bPtr[1] = 20
bPtr[2] = 30
bPtr[3] = 40

Pointer/offset notation
*(bPtr + 0) = 10
*(bPtr + 1) = 20
*(bPtr + 2) = 30
*(bPtr + 3) = 40
