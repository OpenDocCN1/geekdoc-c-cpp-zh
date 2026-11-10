
- return more than one value from a function indirectly
- pass arrays and strings more conveniently from one function to another
- manipulate arrays more easily by moving pointers to them (or to parts of them) instead of moving the arrays themselves
- create complex data structures, such as linked lists and binary trees, where one data structure must contain references to other data structures
- communicate information about memory, as in the function malloc(), which returns the location of free memory by using a pointer
- compile faster, more efficient code than other derived data types such as arrays

Therefore, a pointer variable is a variable that stores the address of another variable. In C, there is an additional restriction on pointers—they are not allowed to store any memory address, but they can only store addresses of variables of a given type.

## 13.4.1 Declaring a Pointer

Just as any other variable in a program, a pointer has to be declared; it will have a value, a scope, a lifetime, a name; and it will occupy a certain number of memory locations. The pointer operator available in C is `*`, called value at address operator. It returns the value stored at a particular address. The value at address operator is also called indirection operator. A pointer variable is declared by preceding its name with an asterisk. The syntax for declaring a pointer variable is

```
datatype * pointer_variable;
```

where datatype is the type of data that the pointer is allowed to hold the address of (that is, the type of data that the pointer is allowed to point to) and pointer_variable is the pointer variable name that is used to refer to the address of a variable of type datatype.

An example of a pointer declaration would be

```
char *ptr;
```

The above declaration should be evaluated as: ptr is a pointer to char type data. char is not the data type of ptr. ptr is an identifier of type pointer and char is a data specifier that is used to indicate the type of data at the memory address that ptr is holding. Pointers are variables that hold memory addresses. At the memory address, which is held in a pointer, a value is stored; this value may be of primitive or user-defined data type. In declaring a pointer variable, the programmer is actually declaring a variable that holds a memory address that points to a specific type of data value. Consider the following declaration.

```
int *a;
```

This declaration indicates that a is a pointer type variable that points to int type data. That is, the int indicates that the pointer variable is intended to store the address of an integer variable. Such a pointer is said to 'point to' an integer.

```
float *t;
```

The above declaration represents the fact that t is a pointer type variable that points to float type data. Some declarations are listed in Table 13.2.

Table 13.2 Meaning of some pointer type variable declarations

| Declaration | What it means |
|---|---|
| int p | p is an integer |
| int *p | p is a pointer to an integer |
| char p | p is a character |
| char *p | p is a pointer to a character |
| long p | p is a long integer |
| long *p | p is a pointer to a long integer |
| unsigned char p | p is an unsigned character |
| unsigned char *p | p is a pointer to an unsigned character |

Consider the following program.

```c
#include <stdio.h>
int main()
{
    int *p;
    float *q;
    double *r;
    printf("\n the size of integer pointer is %d", sizeof(p));
    printf("\n the size of float pointer is %d", sizeof(q));
    printf("\n the size of double pointer is %d", sizeof(r));
    printf("\n the size of character pointer is %d", sizeof(char *));
    return 0;
}
```

Output

```text
In Turbo C

the size of integer pointer is 2
the size of float pointer is 2
the size of double pointer is 2
the size of character pointer is 2

In GCC

the size of integer pointer is 4
the size of float pointer is 4
the size of double pointer is 4
the size of character pointer is 4
```

The output shows that all the pointer type variables (p, q, and r) take up the same storage space. Depending upon the machine architecture, the size of a pointer will range from being a 16-bit field on the IBM PC class of machines, to a 64-bit field on a Cray supercomputer.

### Why should pointers have data types?

Let it be assumed that an address in a hypothetical machine is 32 bits long. The addressing of a byte or word will, therefore, require a 32-bit address. This suggests that a pointer (as pointers store addresses) should be capable of storing at least a 32-bit value irrespective of whether it is an integer or a character. This brings in a question. Why should pointers have data types when their size is always four bytes (in a 32-bit machine) irrespective of the target they are pointing to?

Before discussing why pointers should have data types, it would be beneficial to understand the following points about C.

- C has data types of different size, i.e., objects of different types will have different memory requirements.
- It supports uniformity of arithmetic operations across different (pointer) types.
- It does not maintain data type information in the object or executable image.

When objects of a given data type are stored consecutively in the memory (that is, an array), each object is placed at a certain offset from the previous object, if any, depending on its size. A compiler that generates a code for a pointer, which accesses these objects using pointer arithmetic, requires information on generating offset. The data type of the pointer provides this information. This explains the first point.

The second point is reasonable enough to suggest that pointers should have data types. Sizes of various data types are basically decided by the machine architecture and/or the implementation. Moreover, if arithmetic operations were not uniform, then the responsibility of generating proper offset for accessing array elements would completely rest on the programmer. This has the following drawbacks.

- A programmer is likely to commit mistakes such as typographical mistakes and providing wrong offsets.
- Porting the code to other implementations would require changes, if data type sizes differ. This would lead to portability issues.

### Note

- Pointers have data types but the size of a pointer variable is always four bytes (in a 32-bit machine) whatever the data type used in declaring it.

### Where is a pointer stored?

A pointer can be stored in any location like any other variable, but is generally not stored on the heap. It can be defined and stored globally, or it can be defined local to a function and stored on the stack. The size of the pointer depends on the implementation and for 32-bit operating systems, it generally requires four bytes of storage space. This is, however, not a requirement. A compiler writer can use any number of bytes desired to store a pointer.

Keep in mind that a pointer is like any other variable in the sense that it requires storage space somewhere in the computer’s memory, but it is not like most variables because it contains no data, only an address. Since it is an address, it actually contains a number referring to some memory location. Dynamically allocated arrays can also be expanded during the execution of the program.

## 13.4.2 Initializing Pointers

It should be noted that, unlike a simple variable that stores a value, a pointer must be initialized with a specified address prior to its use. One of the most common causes of errors in programming by novices and professionals alike is uninitialized pointers. These errors can be very difficult to debug because the effect of the errors is often delayed until later in the program execution. Consider the following program.

```c
#include <stdio.h>
int main()
{
    int *p;        /* a pointer to an integer */
    printf("%d\n", *p);
    return 0;
}
```

This code conveys to the compiler to print the value that p points to. However, p has not been initialized yet; it contains the address 0 or some random address. A pointer must not be used until it is assigned a meaningful address. To use a pointer that has not been initialized properly will cause unpredictable results. When a program starts execution, an uninitialized pointer will have some unknown memory addresses in it. More precisely, it will have an unknown value that will be interpreted as memory addresses. To use a pointer that has not been initialized properly will cause unpredictable results. In most cases, a segmentation fault (or some other run-time error) results, which means that the pointer variable used points to an invalid area of memory. Sometimes the program will appear to run correctly but when the program terminates, the message ‘Null Pointer Assignment’ will be displayed. This message notifies the programmer that the program is using an uninitialized pointer. In other cases, the use of an uninitialized pointer will result in a ‘Bus Error’ or
