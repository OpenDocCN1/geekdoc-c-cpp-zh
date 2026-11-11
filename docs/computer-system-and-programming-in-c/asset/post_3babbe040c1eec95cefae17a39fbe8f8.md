
to a pointer variable, which will store the address of the allocated memory.
If memory allocation failed (for example, if you are out of memory), malloc will return a NULL pointer.

## Example

The standard method of creating an array of ten int objects:
`int array[10];`
To allocate a similar array dynamically, the following code could be used:

```c
/* Allocate space for an array with ten elements of type int. */
int *ptr = malloc(10 * sizeof (int));
if (ptr == NULL) {
    /* Memory could not be allocated, the program should handle the error here as appropriate. */
} else {
    /* If ptr is not NULL, allocation succeeded. */
}
```

malloc returns NULL to indicate that no memory is available, or that some other error occurred which prevented memory being allocated.

## Programming Problem

### Problem 1

Write a program to input how many numbers and then input the numbers and then print the maximum number between them with the help of malloc function.

#### Solution

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, max;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) malloc(n*sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    max=p[0];
    for(i=1;i<n;i++)
    {
        if(max<p[i])
            max=p[i];
    }
    printf("\n the maximum number is %d",max);
    getch();
}
```

### Problem 2

Write a program to input how many numbers and then input the numbers and then print the minimum number between them with the help of malloc function.

#### Solution

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, min;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) malloc(n*sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    min=p[0];
    for(i=1;i<n;i++)
    {
        if(min>p[i])
            min=p[i];
    }
    printf("\n the minimum number is %d", min);
    getch();
}
```

### Problem 3

Write a program to input how many numbers and then input the numbers and then print the sum of all the numbers with the help of malloc function?

#### Solution

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, sum=0;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) malloc(n*sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    for(i=0;i<n;i++)
    {
        sum=sum+p[i];
    }
    printf("\n the sum is %d",sum);
    getch();
}
```

## (b) calloc() Function

The `calloc` function allocates space for an array of `n` number objects, each of whose size is `size`. The space is initialized to all bits zero.

The standard C library declares the function `calloc()` as follows:

`void * calloc(size_t elements, size_t sz);`

We can also define the syntax of `calloc()` function as follows:

`<Pointer variable> = (<data type*>) calloc (no of elements, size of (data type));`

`calloc()` allocates space for an array of elements, each of which occupies `sz` bytes of storage. The space of each element is initialized to binary zeros. In other words, `calloc()` is similar to `malloc()`, except that it handles arrays of objects rather than a single chunk of storage and that it initializes the storage allocated. The following example allocates an array of 100 int’s using `calloc()`:

`int *p = (int*) calloc (100, sizeof(int));`

## Programming Problem

### Problem 1

Write a program to input how many numbers and then input the numbers and print the maximum number between them with the help of calloc function.

#### Solution

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, max;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) calloc(n,sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    max=p[0];
    for(i=1;i<n;i++)
    {
        if(max<p[i])
            max=p[i];
    }
    printf("\n the maximum number is %d", max);
    getch();
}
```

### Problem 2

Write a program to input how many numbers and then input the numbers and then print the minimum number between them with the help of calloc function.

#### Solution

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, min;
    clrscr();
    printf("\n enter how many elements");
    scanf("%d",&n);
    p=(int *) calloc(n,sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    min=p[0];
    for(i=1;i<n;i++)
    {
        if(min>p[i])
            min=p[i];
    }
    printf("\n the minimum number is %d", min);
    getch();
}
```

### Problem 3

Write a program to input how many numbers and then input the numbers and then print the sum of all the numbers with the help of calloc function.

#### Solution

```c
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
void main()
{
    int *p, n, i, sum=0;
    clrscr();
    printf("\n enter how many elements");
    scanf ("%d", &n);
    p=(int *) calloc(n, sizeof(int));
    for(i=0;i<n;i++)
    {
        printf("\n enter the element");
        scanf("%d",&p[i]);
    }
    for(i=0;i<n;i++)
    {
        sum=sum+p[i];
    }
    printf("\n the Sum is %d",sum);
    getch();
}
```

## Difference between malloc() and calloc() Function

Both the malloc() and the calloc() functions are used to allocate dynamic memory. Each operates slightly different from the other. malloc() takes a size and returns a pointer to a chunk of memory that is at least that big: `void *malloc( size_t size );` calloc() takes a number of elements, and the size of each, and returns a pointer to a chunk of memory at least big enough to hold them all:

`void *calloc( size_t numElements, size_t sizeOfElement );`

There is one major difference and one minor difference between the two functions. The major difference is that malloc() does not initialize the allocated memory. The first time malloc() gives you a particular chunk of memory, the memory might be full of zeros. If memory has been allocated, freed, and reallocated, it probably hasn't been left zeroed. That means, unfortunately, that a program might run in simple cases (when memory is never reallocated) but break when used harder (and when memory is reused). calloc() fills the allocated memory with all zero bits. That means that anything you're going to use as a char or an int of any length, signed or unsigned, is guaranteed to be zero. Anything you're going to use as a pointer is set to all zero bits. That is usually a null pointer, but it is not guaranteed. Anything you are going to use as a float or double is set to all zero bits; that is a floating-point zero on some types of machines, but not on all.

The minor difference between the two is that calloc() returns an array of objects; malloc() returns one object. Some people use calloc() to make clear that they want an array.

## (c) free() Function

When you allocate memory with either malloc() or calloc(), it is taken from the dynamic memory pool that is available to your program. This pool is sometimes called the heap, and it is finite. When your program finishes using a particular block of dynamically allocated memory, you should deallocate, or free, the memory to make it available for future use. To free memory that was allocated dynamically, use free(). Its prototype is

`void free(void *ptr);`

The free() function releases the memory pointed to by ptr. This memory must have been allocated with malloc(), calloc(), or realloc(). If ptr is NULL, free() does nothing.

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_266_0.png)

From the above Fig. (a), it is clear that the size of the stack is 4 locations and that Sp = -1 indicates that the stack is empty and we can push the new items into the stack. Now Fig. (b) shows how the stack grows when we push elements 12, 13, and 14 onto the stack. Figure (c) shows the status of the stack after popping 2 times. Now performing one more pop operation on the above stack causes an error known as “stack underflow”. Figure (d) shows the content of the stack after pushing 16, 17, 18, and 19. If you try to add one more element, the stack generates an error “stack overflow”.

**Note:** We can also refer to `SP` as the stack pointer.

## OPERATIONS OF STACK

There are two operations applied on stack, they are:

- Push
- Pop

### 1. Push

Push operation is used to insert a new element into the stack. At the time of insertion first check the stack is full or not. If the stack is full it generates an error message “stack overflow”.

### 2. Pop

Pop operation is used to delete an element from the stack. At the time of deletion first check the stack is empty or not. If the stack is empty it generates an error message “stack underflow”.

### Algorithms for Push and Pop Function

#### Assumptions

- `sp` stack pointer whose initial value is -1
- `max_stack` is the size of the stack
- `stack[]` is an array
- `element` is the element to be added or deleted

#### Algorithm to push an element into the stack

```
Step: 1) Start
Step: 2) Take the element to push into stack
Step: 3) If (Sp == max_stack)
Display “The stack is full”
Else
{
    Sp = Sp + 1
    stack[Sp] = item
}
Step: 4) Return to main program
```

#### Algorithm to pop an element from the stack

```
Step: 1) Start
Step: 2) If (Sp == -1)
Display “stack is empty”
Else
{
    element = stack[Sp]
    Sp = Sp - 1
}
Step: 3) Return element
```

### Programming Problems

#### Problem 1

The program given below implements the stack data structure using an array. In this program the elements are pushed into array `stack[]` through `push()` function. The parameters passed to `push()` are the base address of the array, the position in the stack at which the element is to be placed and the element itself. Care is taken by the `push()` function that the user does not try to place the element beyond the bounds of the stack. This is done by checking the value stored in pos. `pop()` function pops out the last element stored in the `stack[]`. Because, top holds the position which has the last element in the stack.

This problem is also called as static implementation of stack or array implementation of stack.

```c
/* To pop and push items in a stack */
#include<stdio.h>
```
