
In DOS and other systems without virtual memory, the limit is set either when the program is compiled or when it begins executing. In UNIX and other systems with virtual memory, the limit is set by the system, and it is usually so large that the programmer can ignore it.

The third and final area does not actually store variables, but can be used to store data pointed to by variables.

Pointer variables that are assigned to the result of a call to the `malloc()` function contain the address of a dynamically allocated area of memory. This memory is in an area called the *heap*. When the program requests a block of data, the dynamic allocation scheme carves out a block from the heap and assigns it to the user by returning a pointer to the beginning of the block. When the system has finished using the block, it returns the block to the heap where it is returned to the pool of available memory called the free list. This is called de-allocation. The heap can share a memory segment with either the data segment or the stack, or it can have its own segment. It all depends on the compiler options and operating system. The heap, like the stack, has a limit on how much it can grow, and the same rules apply as to how that limit is determined.

Since readers are interested only in the logical assignment of memory, they can ignore all of these extra considerations, and still write efficient, robust programs. Compiler writers must keep track of all of these entities in order to make the programmer's job easier. C uses pointers in three main ways.

- (i) Pointers in C provide an alternative means of accessing information stored in arrays, which is especially valuable when working with strings. There is an intimate link between arrays and pointers in C.
- (ii) C uses pointers to handle *variable parameters* passed to functions.
- (iii) They are used to create *dynamic data structures*, that are built up from blocks of memory allocated from the heap at run time. This is only visible through the use of pointers.

Table 13.1 describes the memory layout of the memory elements of a C program.

**Table 13.1 Memory layout summary**

| Memory Section Name | Description |
| --- | --- |
| Text (or the code segment) | This is the area of memory that contains the machine instructions corresponding to the compiled program. This area is READ ONLY and is shared by multiple instances of a running program. |
| Data | This area in the memory image of a running program contains storage for *initialized global variables*. This area is separate for each running instance of a program. |

**Table 13.1 Contd**

| Memory Section Name | Description |
| --- | --- |
| BSS | This is the memory area that contains storage for *uninitialized global variables*. It is also separate for each running instance of a program. |
| Stack | This region of the memory image of a running program contains storage for the automatic (local) variables of the program. It also stores context-specific information before a function call, e.g., the value of the instruction pointer (program counter) register before a function call is made. On most architectures, the stack grows from *higher memory* to *lower memory addresses*. |
| Heap | This memory region is reserved for dynamically allocating memory for variables at run time. Dynamic memory allocation is done by using the `malloc` or `calloc` functions. |
| Shared libraries | This region contains the executable image of shared libraries being used by the program. |

## 13.3 ADDRESS OF OPERATOR (&)

Readers might have noticed that when we call certain functions in C the & sign is used. For example,

```c
scanf("%d", &n);
```

takes the input from the terminal and stores it in integer format in the variable named n. The & sign indicates the address in memory of the integer n, which must be previously declared using

```c
int n;
```

where the function stores the inputted data. Just like a house address in a town, the memory address is an integer specifying the location where something resides. `scanf` needs to know this in order to redirect the data. If one forgets and types `n` instead, the `scanf` function interprets the actual integer value of `n` as an address and tries to send its output there. This address may not exist, it may be used by the operating system or otherwise blocked, or it may be impossible to find again. It is likely to get a

`segmentation fault`

error when one compiles, and certainly get nonsense values if the program runs.

To recap, the compiler considers `n` as the value of `n` (which will be junk if it has not been assigned yet) and `&n` as `n`'s address. At the moment when the variable is declared, it must be stored in a concrete location in the succession of cells in the memory. The programs do not decide where the variable is to be placed. It is done automatically by the compiler and the operating system at run time. But once the operating system has assigned an address there may be cases where it may be of interest to know the location of the variable. This can be done by preceding the variable identifier by an ampersand (&), which literally means ‘address of’.

Now, the above ideas are illustrated with some more details. Consider the declaration,

```c
int i = 3;
```

This declaration tells the C compiler to

- reserve space in memory to hold the integer value
- associate the name i with this memory location
- store the value 3 at this location

i’s location in the memory may be logically represented with the memory map shown in Fig. 13.2.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_344_0.png)

**Fig. 13.2** Memory map

The computer has selected memory location 21474878276 as the place to store the value 3. This location number 21474878276 is not a number to be relied upon, because at some other time the computer may choose a different location for storing the value 3. This address can be printed using the following statement:

```c
printf("\n Address of i = %u", &i);
```

The output will be: 21474878276. Look at the printf() statement carefully. The ‘&’ used in this statement is C’s address operator. The expression &i returns the address of the variable i, which in this case happens to be 21474878276.

The address is printed using %u control string as it is of type unsigned int. %X can also be used. Actually %p should be used because it prints the input argument as a memory address.

```c
printf("\n Address of i = %x", &i);
```

will print FFDC in hexadecimal as the address of variable ‘i’.

### Why an unassigned pointer should not be used?

According to an elementary school verse, “I shot an arrow into the air, where it lands, I don’t care.” It may rhyme, but its message is really not appropriate for little ones. However, when a pointer is declared and then used without first assigning it a value, it does the programming equivalent of the verse.

The following program declares a pointer and then attempts to output its value without first assigning it a value.

```c
#include <stdio.h>
int main()
{
    int *ptr;
    printf("\n The value of ptr is %u", ptr);
    return 0;
}
```

The result, depending on the compiler and operating system, may be a compiler error, a run-time error, or a computer that locks up. Regardless, attempting to use a declared pointer without first assigning it a value is not a good idea.

It may be recalled from previous chapters that when a variable is declared and then an attempt is made to output its value without first assigning it a value, the result is a so-called garbage value that makes little sense. The reason for this result is that the computer attempts to interpret whatever value is left over from previous programs at the address of the variable.

When the variable is a pointer, that leftover value is interpreted as another memory address, which the pointer then tries to access when we attempt to use it. There are a number of memory address ranges that are not permitted to access programmatically, such as those reserved for use by the operating system. If the leftover value is interpreted as one of those prohibited addresses, the result is an error.

**Note**

- After declaring a variable, where the variable is to be located is decided by the compiler and the operating system at run time.
- After declaring a variable, if an attempt is made to output its value without assigning a value, the result is a garbage value.

## 13.4 POINTER

A pointer provides a way of accessing a variable without referring to the variable directly. The mechanism used for this is the address of the variable. A program statement can refer to a variable indirectly using the address of the variable.

A pointer variable holds the memory address of another variable. Put another way, the pointer does not hold a value in the traditional sense; instead, it holds the address of another variable. They are called pointers for the simple reason that by storing an address, they ‘point’ to a particular point in memory. A pointer points to that variable by holding a copy of its address. Because a pointer holds an address rather than a value, it has two parts. The pointer itself holds the address. The address points to a value.

Pointers can be used to:

- call by address, thereby facilitating the changes made to a variable in the called function to become permanently available in the function from where the function is called
