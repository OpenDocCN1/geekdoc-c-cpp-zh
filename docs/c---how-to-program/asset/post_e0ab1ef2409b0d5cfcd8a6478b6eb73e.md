
> **Portability Tip 7.1**
> *The number of bytes used to store a particular data type may vary between systems. When writing programs that depend on data type sizes and that will run on several computer systems, use sizeof to determine the number of bytes used to store the data types.*

Operator sizeof can be applied to any variable name, type or value (including the value of an expression). When applied to a variable name (that's not an array name) or a constant, the number of bytes used to store the specific type of variable or constant is returned. The parentheses are required when a type is supplied as sizeof's operand.

## 7.8 Pointer Expressions and Pointer Arithmetic

Pointers are valid operands in arithmetic expressions, assignment expressions and comparison expressions. However, not all the operators normally used in these expressions are valid in conjunction with pointer variables. This section describes the operators that can have pointers as operands, and how these operators are used.

### 7.8.1 Allowed Operators for Pointer Arithmetic

A pointer may be incremented (++) or decremented (--), an integer may be added to a pointer (+ or +=), an integer may be subtracted from a pointer (- or -=) and one pointer may be subtracted from another—this last operation is meaningful only when both pointers point to elements of the same array.

### 7.8.2 Aiming a Pointer at an Array

Assume that array `int v[5]` has been defined and its first element is at location 3000 in memory. Assume pointer variable vPtr has been initialized to point to v[0]—i.e., the value of vPtr is 3000. Figure 7.18 illustrates this situation for a machine with 4-byte integers. Variable vPtr can be initialized to point to array v with either of the statements

```c
vPtr = v;
vPtr = &v[0];
```

> **Portability Tip 7.2**
> *Because the results of pointer arithmetic depend on the size of the objects a pointer points to, pointer arithmetic is machine and compiler dependent.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_327_0.png)

Fig. 7.18 | Array v and a pointer variable vPtr that points to v.

### 7.8.3 Adding an Integer to a Pointer

In conventional arithmetic, 3000 + 2 yields the value 3002. This is normally *not* the case with pointer arithmetic. When an integer is added to or subtracted from a pointer, the pointer is *not* incremented or decremented simply by that integer, but by that integer times the size of the object to which the pointer refers. The number of bytes depends on the object’s data type. For example, the statement

```c
vPtr += 2;
```

would produce 3008 (3000 + 2 * 4), assuming an integer is stored in 4 bytes of memory. In the array *v*, *vPtr* would now point to *v[2]* (Fig. 7.19). If an integer is stored in 2 bytes of memory, then the preceding calculation would result in memory location 3004 (3000 + 2 * 2). If the array were of a different data type, the preceding statement would increment the pointer by twice the number of bytes that it takes to store an object of that data type. When performing pointer arithmetic on a character array, the results will be consistent with regular arithmetic, because each character is 1 byte long.

> **Common Programming Error 7.4**
>
> *Using pointer arithmetic on a pointer that does not refer to an element in an array.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_328_0.png)

**Fig. 7.19** | The pointer vPtr after pointer arithmetic.

### 7.8.4 Subtracting an Integer from a Pointer

If *vPtr* had been incremented to 3016, which points to *v[4]*, the statement

```c
vPtr -= 4;
```

would set *vPtr* back to 3000—the beginning of the array.

> **Common Programming Error 7.5**
>
> *Running off either end of an array when using pointer arithmetic.*

### 7.8.5 Incrementing and Decrementing a Pointer

If a pointer is being incremented or decremented by one, the increment (++) and decrement (--) operators can be used. Either of the statements

```c
++vPtr;
vPtr++;
```

increments the pointer to point to the *next* location in the array. Either of the statements

```c
--vPtr;
vPtr--;
```

decrements the pointer to point to the *previous* element of the array.

### 7.8.6 Subtracting One Pointer from Another

Pointer variables may be subtracted from one another. For example, if vPtr contains the location 3000, and v2Ptr contains the address 3008, the statement

```c
x = v2Ptr - vPtr;
```

would assign to x the *number of array elements* from vPtr to v2Ptr, in this case 2 (not 8). Pointer arithmetic is undefined unless performed on an array. We cannot assume that two variables of the same type are stored contiguously in memory unless they’re adjacent elements of an array.

![](img/d0d3b7423c2d9e5650be79209ea1885d_329_0.png)

> **Common Programming Error 7.6**
>
> *Subtracting two pointers that do not refer to elements in the same array.*

### 7.8.7 Assigning Pointers to One Another

A pointer can be assigned to another pointer if both have the *same type*. The exception to this rule is the pointer to void (i.e., `void *`), which is a generic pointer that can represent *any* pointer type. All pointer types can be assigned a pointer to void, and a pointer to void can be assigned a pointer of any type (including another pointer to void). In both cases, a cast operation is *not required*.

### 7.8.8 Pointer to void

A pointer to void *cannot* be dereferenced. Consider this: The compiler knows that a pointer to int refers to 4 bytes of memory on a machine with 4-byte integers, but a pointer to void simply contains a memory location for an *unknown* data type—the precise number of bytes to which the pointer refers is *not* known by the compiler. The compiler *must know* the data type to determine the number of bytes that represent the referenced value.

![](img/d0d3b7423c2d9e5650be79209ea1885d_329_1.png)

> **Common Programming Error 7.7**
>
> *Assigning a pointer of one type to a pointer of another type if neither is of type `void *` is a syntax error.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_329_2.png)

> **Common Programming Error 7.8**
>
> *Dereferencing a `void *` pointer is a syntax error.*

### 7.8.9 Comparing Pointers

Pointers can be compared using equality and relational operators, but such comparisons are meaningless unless the pointers point to elements of the *same* array. Pointer comparisons compare the addresses stored in the pointers. A comparison of two pointers pointing to elements in the same array could show, for example, that one pointer points to a higher-numbered element of the array than the other pointer does. A common use of pointer comparison is determining whether a pointer is NULL.

![](img/d0d3b7423c2d9e5650be79209ea1885d_330_0.png)

> **Common Programming Error 7.9**
>
> *Comparing two pointers that do not refer to elements in the same array.*

## 7.9 Relationship between Pointers and Arrays

Arrays and pointers are intimately related in C and often may be used interchangeably. An array name can be thought of as a constant pointer. Pointers can be used to do any operation involving array indexing.

Assume the following definitions:

```c
int b[5];
int *bPtr;
```

Because the array name b (without an index) is a pointer to the array's first element, we can set bPtr equal to the address of the array b's first element with the statement

```c
bPtr = b;
```

This statement is equivalent to taking the address of array b's first element as follows:

```c
bPtr = &b[0];
```

### 7.9.1 Pointer/Offset Notation

Array element b[3] can alternatively be referenced with the pointer expression

```c
*(bPtr + 3)
```

The 3 in the expression is the offset to the pointer. When bPtr points to the array's first element, the offset indicates which array element to reference, and the offset value is identical to the array index. This notation is referred to as pointer/offset notation. The parentheses are necessary because the precedence of `*` is higher than the precedence of `+`. Without the parentheses, the above expression would add 3 to the value of the expression `*bPtr` (i.e., 3 would be added to b[0], assuming bPtr points to the beginning of the array). Just as the array element can be referenced with a pointer expression, the address

```c
&b[3]
```

can be written with the pointer expression

```c
bPtr + 3
```

The array itself can be treated as a pointer and used in pointer arithmetic. For example, the expression

```c
*(b + 3)
```

also refers to the array element b[3]. In general, all indexed array expressions can be written with a pointer and an offset. In this case, pointer/offset notation was used with the name of the array as a pointer. The preceding statement does not modify the array name in any way; b still points to the first element in the array.
