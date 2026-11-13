
## A pointer to an array

The format for creating a pointer to an array:

```
data_type (*pointer_name) [size];
```

where the data-type should match the data type it points to; the size within bracket equals to the number of columns and pointer_name is the name of the pointer.

The objective of declaring a pointer to an array is to ensure that the unit increment of the corresponding pointer always takes from beginning of one row to the beginning of next row, independent of the data type. Remember that pointer to an array is different from the array of pointer.

### Example

```
int a[3][4] = {{11, 12, 13, 14},
{21, 22, 23, 24},
{31, 32, 33, 34}};

int (*p) [4];
int i, j;
p = a;
for(i=0;i<3;i++)
{
for(j=0;j<4;j++)
printf("%5d", p[i] [j]);
printf("\n");
}
```

Here, the pointer to an array of size 4 is declared that should be equal to the column size of the two-dimensional array. The base address of the array is assigned to the pointer variable p. The pointer variable p can be used just like as it is an array name and the printf statement outputs the value of the each element of the array.

## Pointer to Function

Pointers can point to integer, character, array, pointer as well as pointers can also point to the C function. The functions are loaded into computer memory before they are invoked by the program. Therefore, they have also addresses, from where they are loaded into the memory. When a function address is known then a pointer can point to it. The pointer can provide another way to invoke the function. Note that, the function name itself is an address of the function.

The format for creating a pointer to a function:

```
data_type (*pointer_name) ();
```

where data_type same as the return type of the function and pointer_name is the name of the pointer that points to a function.

### Example

```
#include <stdio.h>
main()
{
int (*p) ();
p = show;
printf("Address of Function show is %u\n", show);
/* Function show is called using pointer */
(*p)();
int show()
{
printf("Hello India!");
return 0;
}
Output:
Address of Function show is 4198701
Hello India!
```

Pointers can point to user-defined functions as well as they can point to library functions.
The uses of the pointer to the function are as follows:

- To write memory resident programs.
- To write viruses (i.e. Worms, Trojan horses, etc.) and vaccines (i.e. anti-virus) to remove viruses.

## Passing Addresses to Function

A function can pass a value, as well as it can pass addresses to the function i.e. can pass a reference.
The addresses of actual arguments in the calling function are copied to formal arguments of the called function. The addresses of the actual arguments are copied to formal arguments as a value, not a reference. In C language functions are called by value and C does not support reference data types. That means the called function uses the values of its arguments as temporary variables rather than the originals. When the temporary variables are modified in the called function, then it has no effect on the actual arguments in the calling function.

It is possible to create a function that can modify a variable in the calling function. Generally, a function can return only one value to the calling function. However, a function can return more than one value at a time to the calling function by passing addresses. The calling function passes the addresses of the variables and the called function must declare the arguments to be a pointer and access the variable indirectly through it.

### Example

```
#include <stdio.h>
void swap(int *a, int *b);
main()
{
int i = 10, j = 20;
printf("Before calling function i = %d, j = %d\n", i, j);
swap(&i, &j);
printf("After calling function i = %d, j = %d\n", i, j);
}
void swap(int *a, int *b)
{
int temp;
temp = *a;
*a = *b;
*b = temp;
}
Output:
Before calling function i = 10, j = 20
After calling function i = 20, j = 10
```

## Function Returning Pointer

The functions can return an integer, a floating point or any other data type; as well as it can also return a pointer. To create a function returning a pointer should explicitly mention in the function prototype and in the function definition.

The format of function returning pointer:

```
data-type *function-name (argument-list)
```

### Example

```
#include <stdio.h>
#include <stdlib.h>
char *xstrcat(char *,char *);
main()
{
char *dest, *source = "India!", *target = "Hello ";
dest=xstrcat(target, source);
printf("source = %s\n",source);
printf("target = %s\n",target);
printf("dest = %s\n",dest);
}
char *xstrcat(char *t,char *s)
{
int i;
char *temp;
temp=(char *)malloc(25);
for(i=0; *(t+i)!='\0';i++)
*(temp+i)=*(t+i);
while(*s)
{
*(temp+i)=*s;
*s++;
i++;
}
return(temp);
}
Output:
source = India!
target = Hello
dest = Hello India!
```

## Dynamic Memory Allocation

When memory has been needed by a program, it has been set aside by declaring the desired type of variables. For variables declared in any function, space in memory is set aside to hold the value assigned to the variable. This memory is reserved until the function finishes.

Another problem may arise when declared an array in a program. The user may provide a less number of elements than the number of elements of the declared array, and then the rest of the memory space will be wasted. This leads to the inefficient use of memory. As well as the user may also enter a number of elements more than the number of elements of the declared array, then the user may get unexpected result or user may face a runtime error or system may be crashed.

This may not always be the optimal way to allocate memory. Fortunately, you can instead write your programs and obtain memory as they are running. With dynamic memory allocation, memory is not reserved or set aside at the start of the program; rather, it is allocated on an-as-needed basis.

When a program is compiled, many memory locations needed for the program to hold variable and constant data can be determined in advance. As the compiler works through the main part of the program and each of the other functions, it can figure out how much memory will be needed when the program runs. The memory can be divided into four regions as shown in the figure.

When the program is loaded, it can request the needed memory from the operating system before the program actually begins to run. The operating systems reserve the needed memory locations by stacking one variable on top of another in memory, in a tight, neat block. Because of the way this process works, this part of the memory is known as the stack. Memory reserved within the stack cannot be freed up until the program quits running.

| Region |
| :--- |
| Stack |
| Heap |
| Global Variables |
| Program Code |

**Figure 4.5:** Four regions of memory

Some programs need to use a large block of memory to hold data, but they only need those blocks for a short period of time. Rather than use all that memory the entire time the program is running, such programs can temporarily allocate storage locations from another portion of memory, known as the heap. When the program is done using a particular block of heap memory, it simply tells the operating system that it is done, and the system returns that memory to the heap, where it can be freed out to other needing programs. For best utilization of memory, clearly having a heap is a good idea.

A compiled C program creates and uses four logically distinct regions of memory. The first region is memory that actually holds the program's executable code. The next region is a memory where global variables are stored. The remaining two regions are the stack and the heap. The stack is used for a great many things while your program executes. It holds the return addresses of function calls, arguments to functions, and local variables. It will also save the current state of the CPU. The heap is a region of free memory that your program can use via C's dynamic memory allocation functions.
