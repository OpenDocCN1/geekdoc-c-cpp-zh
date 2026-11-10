
```
32. int main()
{
    int a[5]={1,3,6,7,0};
    int *b;
    b=&a[2];
    printf("%d", b[-1]);
    return 0;
}
```

Output: 3

```
33. int main()
{
    register int x=5, *p;
    p=&x;
    printf("%d", *p);
    return 0;
}
```

Output: Error

```
34. int main()
{
    void x(void);
    x();
    return 0;
}
void x(void)
{
    char a[]="HELLO";
    char *b="HELLO";
    char c[10]="HELLO";
    printf("%s %s %s\n", a, b, c);
    printf("%d %d %d\n", sizeof(a), sizeof(b), sizeof(c));
}
```

Output: HELLO HELLO HELLO
6 4 10

sizeof(b) gives the bytes required for storing the pointer b. The other two are the array sizes.

## SUMMARY

Think of memory as an array of cells. Each memory cell has a location/address and contains a value. There is a difference between the address and the contents of a memory cell. A pointer is a variable that contains the address in the memory of another variable. There can be a pointer to any variable type. The unary or monadic operator ‘&’ gives the ‘address of a variable’. The indirection or dereference operator ‘*’ gives the ‘contents of an object pointed to by a pointer’. A pointer to any variable type is an address in memory, which is an integer address. A pointer is definitely not an integer. When a pointer is declared, it does not point anywhere. It must be set to point somewhere before it can be used. Thus, an address must be assigned to the pointer by using an assignment statement or a function call prior to its use. A pointer is bound to a particular data type (void pointer is an exception). For instance, the address of a short int cannot be assigned to a long int pointer. There is a special pointer which is defined to be zero. It is called the NULL pointer.

There are many cases when a passed argument in the function may need to be altered and the new value received back once the function has finished. Other languages do this. C uses pointers explicitly to do this. Other languages mask the fact that pointers also underpin the implementation of this. Pointers provide the solution: Pass the address of the variables to the functions and access address of function.

Pointers and arrays are very closely linked in C. When subscript notation is used, the C compiler generates an executable code that does the following.

- Determines the size of the elements in the array. Let us call that `elemSize`.
- Multiplies `elemSize` by the subscript value. Let us call that offset.
- Adds offset to the address that represents the beginning of the array. This is the address of the element that we want to access.

The address of ARRAY[i] is calculated each time by the compiler as follows.

```
address of ARRAY[i] = ARRAY+i*sizeof(int);
```

The equivalence of arrays and pointers must be understood. Assume that a is an array and i is an integer:

```
a[i] == *(a + i) == *(&a[0] + i) == i[a]
```

Although these are equivalent, it is recommended that i[a] never be written instead of a[i]. However, pointers and arrays are different.

- A pointer is a variable. We can do `pa = a` and `pa++`.
- An array is not a variable. `a = pa` and `a++` are illegal.

When an array is passed to a function what is actually passed is its initial element’s location in memory. Array decays into pointers when passed into function.

The following ‘meaningful’ arithmetic operations are allowed on pointers.

- Add or subtract integers to/from a pointer. The result is a pointer.
- Subtract two pointers to the same type. The result is an int.
- Assigning NULL or any pointer of the same datatype.

Multiplying, adding two pointers, etc. does not make sense.

It is also possible to have arrays of pointers since pointers are variables. Arrays of pointers are a data representation that will cope efficiently and conveniently with variable length text lines. This eliminates:

- complicated storage management
- high overheads of moving lines

Pointers, of course, can be pointed at any type of data object, including arrays.

```
int(*p)[10];
```
is the proper declaration, i.e., p here is a pointer to an array of 10 integers just as it was under the declaration using the array type. Note that this is different from

```
int *p[10];
```
which would make p the name of an array of 10 pointers to type int.

A two-dimensional array is really a one-dimensional array, each of whose elements is itself an array. Array elements are stored row by row. When a two-dimensional array is passed to a function, the number of columns must be specified; the number of rows is irrelevant. The reason for this is pointers again. C needs to know the number of columns in order to jump from row to row in memory.

Consider `int a[5][10]` to be passed in a function.

It is possible to say

```
f(int a[][10]) { . . . . . }
```

or even

```
f(int(*a)[10]) { . . . . . }
```

It needs a parenthesis `(*a)` since `[]` have a higher precedence than `*`.

So,

```
int(*a)[10]; declares a pointer to an array of 10 ints.
int *a[10]; declares an array of 10 pointers to ints.
```

Dynamic memory allocation is a way to defer the decision of how much memory is necessary until the program is actually running, get more if it runs out, or give back memory that the program no longer needs. When memory is allocated, the allocating function (such as `malloc()` and `calloc()`) returns a pointer. The type of this pointer depends on the type of compiler, whether it is an older K&R compiler or the newer ANSI type compiler. With the older compiler the type of the returned pointer is char; with the ANSI compiler it is void. When the program finishes using whatever memory it dynamically allocates, it can use the free function to indicate to the system that the memory is available again.

The rules to be followed for deciphering pointer declarations are as follows. These are particularly important for function pointers.

- Start with the name that will identify the pointer, known as the identifier.
- Move to the right until you encounter a right-parenthesis ')' or reach the end. Do not stop if the () brackets are used to pass parameters to a function. Also do not stop on encountering brackets used with arrays: [ ].
- Now go left of the identifier to continue deciphering the declaration. Keep going left until you find a left-parenthesis '(' or reach the end. Do not stop if the brackets are used to pass parameters to a function.
- The whole interpretation should be a single long sentence.

## KEY TERMS

- **Call by address** It facilitates the changes made to a variable in the called function to become permanently available in the function from where the function is called.
- **Call-by-value** A particular way of implementing a function call, in which the arguments are passed by their value (i.e., their copies).
- **Dangling pointer** A pointer pointing to a previously meaningful location that is no longer meaningful; usually a result of a pointer pointing to an object that is deallocated without resetting the value of the pointer.
- **Dynamic data structures** Those that are built up from blocks of memory allocated from the heap at run time.
- **Dynamic memory allocation** It is the process of requesting and obtaining additional memory segments during the execution of a program.
- **Function pointer** A function has a physical location in memory that can be assigned to a pointer. Thus, it is called function pointer. This address is the entry point of the function and it is the address used when the function is called.
- **Garbage collection** If only implicit dynamic allocation is allowed then deallocation must also be done by implicit means, which is often called garbage collection.
- **Heap** This memory region is reserved for dynamically allocating memory for variables at run time. Dynamic memory allocation is done by using the `malloc()` or `calloc()` functions.
- **Memory leak** A commonly used term indicating that a program is dynamically allocating memory but not properly deallocating it, which results in a gradual accumulation of unused memory by the program to the detriment of other programs, the operating system, and itself.
- **NULL** A special C constant, defined as macro in `stdio.h` as 0 or `(void*)` that can be used as the null value for pointers.
- **Null pointer** A null pointer is a special pointer value that points nowhere. It is initialized with value 0 or NULL.
- **Pointer** A value or a variable with two attributes: (i) an address and (ii) a data type of what should be found at that address.
- **Ragged array** It is an array of pointers whose elements are used to point to arrays of varying sizes.
- **Stack** A data structure resembling a deck of cards; a new item can only be put on top of the deck (the push operation) or removed from the top of the deck (the pop operation).
- **Static memory allocation** It is memory layout for static data prepared by the compiler.
- **Void pointer** It is a special type of pointer that can point to any data type.
