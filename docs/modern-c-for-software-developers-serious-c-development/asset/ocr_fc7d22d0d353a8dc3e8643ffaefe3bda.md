initialized variables that can be changed.

**The BSS Segment:** is also called the uninitialized data segment. BSS stands for *Block Started by Symbol*. This segment is initialized to arithmetic zero by the operating system, before the program starts executing. It contains global and static variables that have not been explicitly initialized to zero.

**The Heap Segment:** This segment of memory is used by the program to allocate dynamic memory using malloc, calloc, realloc or new.

**Stack Segment:** This segment of memory grows downward. It stores local variables and function arguments when functions are called. This memory segment is managed by a stack pointer. The stack segment behaves like a LIFO (*last in, first out*) container. The Stack is said to be exhausted when the stack pointer meets the heap.

We can get the memory layout of a program with `gcc`. Consider the program memory.c:

```
#include <stdio.h>

/* Uninitialized variable stored in the BSS segment */
int global;

// parameter z stored on the stack
int Foo(int z) {
// Initialized static variable stored in the Data Segment
static int i = 100;
// local variable stored on the stack
x = 5;
x += z;

// return value stored on the stackq
return x;
}

int main() {
Foo(5);
// dynamic allocation on the heap
float* y = new float;
free(y);
}
```