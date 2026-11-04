# FIGURE 8.1
Memory layout.

![](bbox=[0.38, 0.12, 0.75, 0.5])

ptr is declared as a pointer variable to type int. Therefore, ptr can hold the memory address of an int variable. In general, if the type of the pointer is T, the type of *T is T. For example, the type of the expression *ptr is int.

Pointer variables can be declared together with other variables of the same type. For example:

```
```c
int *ptr, i, j, k;
```
```

Notice that it is allowed to put the * next to the type (e.g., int* ptr;). In fact, many programmers prefer this style. However, this is not our preference, because it might be confusing when multiple variables are declared. For example, with the declaration:

```
```c
int* p1, p2;
```
```

p1 is declared as pointer, p2 is not.

Also, we prefer to declare the pointer variables first, to distinguish them from the ordinary variables.

As with ordinary variables, when a pointer variable is declared, the compiler allocates memory to store its value. For example, the following program uses the sizeof operator to find out how many bytes ptr allocates:

```
```c
#include <stdio.h>
int main(void)
{
    int *ptr;
    printf("Bytes: %u\n", sizeof(ptr));
    return 0;
}
```
```

A pointer variable allocates the same size, no matter what data type it points to. This value is platform dependent; its typical value is four bytes. Therefore, if we write char *ptr; or float *ptr; or double *ptr; in our example, the output would be the same, that is, 4.