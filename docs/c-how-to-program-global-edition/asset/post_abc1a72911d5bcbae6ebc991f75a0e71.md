
increments the pointer to point to the next location in the array. Either of the statements

```
--vPtr;
vPtr--;
```

decrements the pointer to point to the previous element of the array.

### 7.8.6 Subtracting One Pointer from Another

Pointer variables may be subtracted from one another. For example, if vPtr contains the location 3000, and v2Ptr contains the address 3008, the statement

```
x = v2Ptr - vPtr;
```

would assign to x the number of array elements from vPtr to v2Ptr, in this case 2 (not 8). Pointer arithmetic is undefined unless performed on an array. We cannot assume that two variables of the same type are stored contiguously in memory unless they're adjacent elements of an array.

**Common Programming Error 7.6**
Subtracting two pointers that do not refer to elements in the same array.

### 7.8.7 Assigning Pointers to One Another

A pointer can be assigned to another pointer if both have the same type. The exception to this rule is the pointer to void (i.e., void *), which is a generic pointer that can represent any pointer type. All pointer types can be assigned a pointer to void, and a pointer to void can be assigned a pointer of any type (including another pointer to void). In both cases, a cast operation is not required.

### 7.8.8 Pointer to void

A pointer to void cannot be dereferenced. Consider this: The compiler knows that a pointer to int refers to 4 bytes of memory on a machine with 4-byte integers, but a pointer to void simply contains a memory location for an unknown data type—the precise number of bytes to which the pointer refers is not known by the compiler. The compiler must know the data type to determine the number of bytes that represent the referenced value.

**Common Programming Error 7.7**
Assigning a pointer of one type to a pointer of another type if neither is of type void * is a syntax error.

**Common Programming Error 7.8**
Dereferencing a void * pointer is a syntax error.

### 7.8.9 Comparing Pointers

Pointers can be compared using equality and relational operators, but such comparisons are meaningless unless the pointers point to elements of the same array. Pointer comparisons compare the addresses stored in the pointers. A comparison of two pointers pointing to elements in the same array could show, for example, that one pointer points to a higher-numbered element of the array than the other pointer does. A common use of pointer comparison is determining whether a pointer is NULL.

![](img/bf54db922e6fa8319cba11069e785521_324_0.png)

> Common Programming Error 7.9
> Comparing two pointers that do not refer to elements in the same array.

## 7.9 Relationship between Pointers and Arrays

Arrays and pointers are intimately related in C and often may be used interchangeably. An array name can be thought of as a constant pointer. Pointers can be used to do any operation involving array indexing.

Assume the following definitions:

```
int b[5];
int *bPtr;
```

Because the array name b (without an index) is a pointer to the array's first element, we can set bPtr equal to the address of the array b's first element with the statement

```
bPtr = b;
```

This statement is equivalent to taking the address of array b's first element as follows:

```
bPtr = &b[0];
```

### 7.9.1 Pointer/Offset Notation

Array element b[3] can alternatively be referenced with the pointer expression

```
*(bPtr + 3)
```

The 3 in the expression is the offset to the pointer. When bPtr points to the array's first element, the offset indicates which array element to reference, and the offset value is identical to the array index. This notation is referred to as pointer/offset notation. The parentheses are necessary because the precedence of * is higher than the precedence of +. Without the parentheses, the above expression would add 3 to the value of the expression *bPtr (i.e., 3 would be added to b[0], assuming bPtr points to the beginning of the array). Just as the array element can be referenced with a pointer expression, the address

```
&b[3]
```

can be written with the pointer expression

```
bPtr + 3
```

The array itself can be treated as a pointer and used in pointer arithmetic. For example, the expression

```
*(b + 3)
```

also refers to the array element b[3]. In general, all indexed array expressions can be written with a pointer and an offset. In this case, pointer/offset notation was used with the name of the array as a pointer. The preceding statement does not modify the array name in any way; b still points to the first element in the array.

### 7.9.2 Pointer/Index Notation

Pointers can be indexed like arrays. If bPtr has the value b, the expression

```
bPtr[1]
```

refers to the array element b[1]. This is referred to as pointer/index notation.

### 7.9.3 Cannot Modify an Array Name with Pointer Arithmetic

Remember that an array name always points to the beginning of the array—so the array name is like a constant pointer. Thus, the expression

```
b += 3
```

is invalid because it attempts to modify the array name's value with pointer arithmetic.

> **Common Programming Error 7.10**
> 
> *Attempting to modify the value of an array name with pointer arithmetic is a compilation error.*

### 7.9.4 Demonstrating Pointer Indexing and Offsets

Figure 7.20 uses the four methods we've discussed for referring to array elements—array indexing, pointer/offset with the array name as a pointer, pointer indexing, and pointer/ offset with a pointer—to print the four elements of the integer array b.

```
1  // Fig. 7.20: fig07_20.cpp
2  // Using indexing and pointer notations with arrays.
3  #include <stdio.h>
4  #define ARRAY_SIZE 4
5
6  int main(void)
7  {
8      int b[] = {10, 20, 30, 40}; // create and initialize array b
9      int *bPtr = b; // create bPtr and point it to array b
10
11     // output array b using array index notation
12     puts("Array b printed with:\nArray index notation");
13
14     // loop through array b
15     for (size_t i = 0; i < ARRAY_SIZE; ++i) {
16         printf("b[%u] = %d\n", i, b[i]);
17     }
18
19     // output array b using array name and pointer/offset notation
20     puts("\nPointer/offset notation where\n" "the pointer is the array name");
21
22     // loop through array b
23     for (size_t offset = 0; offset < ARRAY_SIZE; ++offset) {
24         printf("*(b + %u) = %d\n", offset, *(b + offset));
25     }
26     }
```

```
// output array b using bPtr and array index notation
puts("\nPointer index notation");
// loop through array b
for (size_t i = 0; i < ARRAY_SIZE; ++i) {
    printf("bPtr[%u] = %d\n", i, bPtr[i]);
}
// output array b using bPtr and pointer/offset notation
puts("\nPointer/offset notation");
// loop through array b
for (size_t offset = 0; offset < ARRAY_SIZE; ++offset) {
    printf("*(bPtr + %u) = %d\n", offset, *(bPtr + offset));
}
```

```
Array b printed with:
Array index notation
b[0] = 10
b[1] = 20
b[2] = 30
b[3] = 40

Pointer/offset notation where
the pointer is the array name
*(b + 0) = 10
*(b + 1) = 20
*(b + 2) = 30
*(b + 3) = 40

Pointer index notation
bPtr[0] = 10
bPtr[1] = 20
bPtr[2] = 30
bPtr[3] = 40

Pointer/offset notation
*(bPtr + 0) = 10
*(bPtr + 1) = 20
*(bPtr + 2) = 30
*(bPtr + 3) = 40
```

Fig. 7.20 | Using indexing and pointer notations with arrays. (Part 2 of 2.)

### 7.9.5 String Copying with Arrays and Pointers

To further illustrate the interchangeability of arrays and pointers, let’s look at the two string-copying functions—copy1 and copy2—in the program of Fig. 7.21. Both functions copy a string into a character array. After a comparison of the function prototypes for copy1 and copy2, the functions appear identical. They accomplish the same task, but they’re implemented differently.

```
1 // Fig. 7.21: fig07_21.c
2 // Copying a string using array notation and pointer notation.
3 #include <stdio.h>
4 #define SIZE 10
5
6 void copy1(char * const s1, const char * const s2); // prototype
7 void copy2(char *s1, const char *s2); // prototype
8
9 int main(void)
10 {
11     char string1[SIZE]; // create array string1
12     char *string2 = "Hello"; // create a pointer to a string
13
14     copy1(string1, string2);
15     printf("string1 = %s\n", string1);
16
17     char string3[SIZE]; // create array string3
18     char string4[] = "Good Bye"; // create an array containing a string
19
20     copy2(string3, string4);
21     printf("string3 = %s\n", string3);
22 }
23
24 // copy s2 to s1 using array notation
25 void copy1(char * const s1, const char * const s2)
26 {
27     // loop through strings
28     for (size_t i = 0; s1[i] = s2[i] != '\0'; ++i) {
29         ; // do nothing in body
30     }
31 }
32
33 // copy s2 to s1 using pointer notation
34 void copy2(char *s1, const char *s2)
35 {
36     // loop through strings
37     for ( ; (*s1 = *s2) != '\0'; ++s1, ++s2) {
38         ; // do nothing in body
39     }
40 }
```

string1 = Hello
string3 = Good Bye

## Fig. 7.21 | Copying a string using array notation and pointer notation.

## Copying with Array Index Notation

Function copy1 uses array index notation to copy the string in s2 to the character array s1. The function defines counter variable i as the array index. The for statement header (line 28) performs the entire copy operation—its body is the empty statement. The header specifies that i is initialized to zero and incremented by one on each iteration of the loop. The expression s1[i] = s2[i] copies one character from s2 to s1. When the null character
