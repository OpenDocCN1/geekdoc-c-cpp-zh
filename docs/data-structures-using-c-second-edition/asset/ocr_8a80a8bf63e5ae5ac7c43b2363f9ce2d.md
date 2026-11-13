of memory of specified size and returns a pointer of type void. This means that we can assign it to any type of pointer. The general syntax of malloc() is

```
ptr = (cast-type*) malloc(byte-size);
```

where ptr is a pointer of type cast-type. malloc() returns a pointer (of cast type) to an area of memory with size byte-size.

For example,

```
arr=(int*)malloc(10*sizeof(int));
```

This statement is used to dynamically allocate memory equivalent to 10 times the area of int bytes. On successful execution of the statement the space is reserved and the address of the first byte of memory allocated is assigned to the pointer arr of type int.

**Programming Tip**
To use dynamic memory allocation functions, you must include the header file stdlib.h.

calloc() function is another function that reserves memory at the run time. It is normally used to request multiple blocks of storage each of the same size and then sets all bytes to zero. calloc stands for contiguous memory allocation and is primarily used to allocate memory for arrays. The syntax of calloc() can be given as:

```
ptr=(cast-type*) calloc(n,elem-size);
```

The above statement allocates contiguous space for n blocks each of size elem-size bytes. The only difference between malloc() and calloc() is that when we use calloc(), all bytes are initialized to zero. calloc() returns a pointer to the first byte of the allocated region.

When we allocate memory using malloc or calloc(), a NULL pointer will be returned if there is not enough space in the system to allocate. A NULL pointer points definitely nowhere. It is a not a pointer marker; therefore, it is not a pointer you can use. Thus, whenever you allocate memory using malloc() or calloc(), you must check the returned pointer before using it. If the program receives a NULL pointer, it should at the very least print an error message and exit, or perhaps figure out some way of proceeding without the memory that was asked for. But in any case, the program cannot go on to use the NULL pointer it got back from malloc()/calloc().

A call to malloc, with an error check, typically looks something like this:

```
int *ip = malloc(100 * sizeof(int));
if(ip == NULL)
{
    printf("\n Memory could not be allocated");
    return;
}
```

Write a program to read and display values of an integer array. Allocate space dynamically for the array.

```
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int i, n;
    int *arr;
    printf("\n Enter the number of elements ");
    scanf("%d", &n);
    arr = (int*)malloc(n * sizeof(int));
    if(arr == NULL)
    {
        printf("\n Memory Allocation Failed");
        exit(0);
    }
}
```