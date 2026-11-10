
## FREQUENTLY ASKED QUESTIONS

### 1. What are the uses of pointers in C?

C uses pointers in three different ways:

- (i) Pointers allow different sections of code to share information easily. One can get the same effect by copying information back and forth, but pointers solve the problem better.
- (ii) In some cases, C programmers also use pointers because they make the code slightly more efficient. Pointers allow the creation of complex dynamic data structures like linked lists and binary trees.
- (iii) Pointers in C provide an alternative way to access information stored in arrays. Pointer techniques are especially valuable while working with strings. There is an intimate link between arrays and pointers in C.

Apart from these, C uses pointers to handle *variable parameters* passed to functions.

### 2. Why should pointers have data types when their size is always 4 bytes (in a 32-bit machine), irrespective of the variable they are pointing to?

Sizes of various data types are basically decided by the machine architecture and/or the implementation. Considering a 32-bit machine, the addressing of a byte or word will, therefore, require a 32-bit address. This suggests that a pointer (as pointers store addresses) should be capable enough to store, at least, a 32-bit value; no matter if it points to an integer or a character.

For an array, consecutive memory is allocated. Each element is placed at a certain offset from the previous element, if any, depending on its size. The compiler that generates code for a pointer, which accesses these elements using the pointer arithmetic, requires the number of bytes to retrieve on pointer dereference and it knows how much to scale a subscript. The data type of the pointer provides this information. The compiler automatically scales a subscript to the size of the variable pointed at. The compiler takes care of scaling before adding the base address.

### 3. What is wrong with the following code segment?

```c
int *p;
*p=10;
```

The pointer p is an uninitialized pointer which may have some unknown memory address in it. More precisely, it may have an unknown value that will be interpreted as a memory location. Most likely, the value will not be valid for the computer system that is using or if it is, will not be valid for the memory that has been allocated. If the address does not exist, one may get immediate run time errors.

### 4. Does C have ‘pass by reference’ feature?

Not really. Strictly speaking, C always uses pass by value. One can simulate pass by reference by defining functions which accept pointers as formal parameters and then using the & operator when calling the function. The compiler will essentially simulate it when an array is passed to a function (by passing a pointer instead). But truly C has no equivalent to the formal pass by reference feature as C++ provides.

### 5. What is wild pointer in C?

A pointer in C which has not been initialized, is known as wild pointer.

### 6. Is a null pointer same as an uninitialized pointer?

A null pointer is conceptually different from an uninitialized pointer. An uninitialized pointer may point to anywhere, whereas a null pointer does not point to any object or function. Null pointer points to the base address of a segment while wild pointer does not point to any specific memory location.

### 7. What are the uses of null pointer?

The null pointer is used for three purposes:

- To stop indirection
- As an error value
- As a sentinel value

### 8. Is NULL always defined as 0?

NULL is defined as either 0 or (void*)0. These values are almost identical; either a literal zero or a void pointer is converted automatically to any kind of pointer, as necessary, whenever a pointer is needed (although the compiler cannot always tell when a pointer is needed).

### 9. What is the difference between NULL and NUL?

NULL is a macro defined in <stddef.h> for the null pointer. NUL is the name of the first character in the ASCII character set. It corresponds to a zero value. NULL can be defined as ((void*)0), whereas NUL is `'\0'`. Both can also be defined simply as 0.

### 10. Since 0 is used to represent the null pointer, can it be thought of as an address with all zero bits?

Each compiler interprets the null pointers differently and not all compilers use a zero address. For example, some compilers use a non-existent memory address for the null pointer; that way, attempting to access memory through a null pointer can be detected by the hardware. When NULL is assigned to a pointer, then 0 is converted to the proper internal form by the compiler.

### 11. What is the difference between arr and &arr where arr is an array name, though both display the base address of the array?

The array name arr is a pointer to the first element in the array whereas the &arr is a pointer to the array as a whole. Numerically, the values they display are same; however, their interpretation is not same.

### 12. When would you use a pointer to a function?

Pointers to functions are typically used when it is required to pass them to other functions. The called function takes function pointers as formal parameters. This is known as a ‘callback’. It is frequently used in graphical-user interface libraries.

### 13. What are the uses of dynamic memory allocations?

Typical uses of dynamic memory allocation are:

- Creation of *dynamic arrays* — arrays whose sizes are chosen at run time.
- Creation of *dynamic data structures* — data collections that grow and shrink with the changing data storage needs of a program or module.

### 14. Why is it required to cast the values returned by malloc() to the pointer type being allocated?

Before ANSI/ISO Standard C introduced the `void *` generic pointer type, these casts were typically required to avoid warnings about assignment between incompatible pointer types. Under ANSI/ISO Standard C, these casts are no more required.

### 15. What happens if `malloc(0)` is called?

If `malloc()` is called with zero size, the result is unpredictable. Each compiler is free to define the behaviour of `malloc()` when the size is 0. It may either return `NULL` or it may return other implementation dependent value.

### 16. What is the difference between `calloc()` and `malloc()`?

`malloc()` takes one argument, whereas `calloc()` takes two. `calloc()` initializes all the bits in the allocated space set to zero, whereas `malloc()` does not do this.

A call to `calloc()` is equivalent to a call to `malloc()` followed by one to `memset()`.

```c
calloc(m, n)
```

is essentially equivalent to

```c
p = malloc(m * n);
memset(p, 0, m * n);
```

### 17. What is a dangling pointer?

A dangling pointer arises when you use the address of an object after its lifetime is over. This may occur in situations like returning addresses of the automatic variables from a function or using the address of the memory block after it is freed.

### 18. Why should NULL be assigned to the pointer after freeing it?

After a pointer has been freed, the pointer can no longer be used. After this memory is freed with the `free()` function, the pointer itself will still contain the address of the (released) block. Such a pointer is referred to as a dangling pointer; it does not point at anything useful. If the pointer is used without reinitializing it, it may or may not run; it merely produces a bug. Such a pointer must be assigned NULL after freeing memory to avoid this bug. The program can no longer get in trouble by using that pointer.

### 19. Is it correct to return a pointer to a local variable in the called function?

Absolutely not; it is an error to return a pointer to a local variable in the called function, because when the function terminates, its memory gets inaccessible.

### 20. What is memory leak?

When memory is allocated dynamically, it is the responsibility of the programmer to deallocate the dynamically allocated memory by calling `free()`. Freeing the memory returns it to the system, where it can be reassigned to another application when needed. When an application dynamically allocates memory, and does not free that memory when it has finished using it, that chunk of memory is still in use to the operating system. The memory is not being used by the application anymore, but it cannot be used by the system or any other program either. This is known as *memory leak*. Memory leaks add up over time, and if they are not cleaned up, the system eventually runs out of memory.

## EXERCISES

- 1. What are pointers? Why are they important?
- 2. Explain the features of pointers.
- 3. Explain the pointer of any data type that requires four bytes.
- 4. Explain the use of `(*)` indirection operator.
- 5. What is a NULL pointer? Is it the same as an uninitialized pointer?
- 6. What is a NULL macro? What is the difference between a NULL pointer and a NULL macro?
- 7. What does the error ‘Null Pointer Assignment’ mean and what causes this error?
- 8. Explain the effect of ++ and -- operators with pointer of all types.
- 9. What is an array of pointer? How is it declared?
- 10. Explain the relation between an array and a pointer.
- 11. Why is the addition of two pointers impossible?
- 12. Which arithmetic operations are possible with pointers?
- 13. Explain the comparison of two pointers.
- 14. How does one pointer point to another pointer?
- 15. How will you recognize pointer to pointer? What does the number of ‘*’s indicate?
- 16. How are strings stored in the pointer variables? Is it essential to declare length?
- 17. What is base address? How is it accessed differently for one-dimensional and two-dimensional arrays?
- 18. Distinguish between the address stored in the pointer and the value at that address.
- 19. Why does the element counting of arrays always start from ‘0’?
- 20. Write a program to read and display a two-dimensional array of 5 by 2 numbers. Reduce the base address of an array by one and start element counting from one.
- 21. How is a pointer initialized?
- 22. Explain the effects of the following statements.

  - (a) `int a, *b=&a;`
  - (b) `int p, *p;`
  - (c) `char *s;`
  - (d) `a = (float*) &x;`
  - (e) `double (*f)();`

- 23. Predict the output of each of the following programs (draw the memory diagram so that it will be easy to answer) where memory addresses are to be described. You can assume any six-digit number. Assume numbers starting from 333333.

  - (a)

    ```c
    int a;
    int *integer_pointer;
    a=222;
    integer_pointer=&a;
    printf("The value of a is %d\n",a);
    printf("The address of a is %d\n",&a);
    ```
