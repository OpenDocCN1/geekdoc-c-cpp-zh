+   b. The address of the next statement is extracted from the stack and the execution of the program continues with that statement.
+   c. The memory allocated to store the function's data is released (not that of static variables, of course).

For example, in the following program, when test() is called, the compiler allocates 808 bytes in the stack to store the values of i, j, and arr elements:

```
#include <stdio.h>

void test(int i, int j);

int main(void)
{
    float a[1000], b[10];
    test(10, 20);
    return 0;
}

void test(int i, int j)
{
    int arr[200];
    ...
}
```

This memory is released when test() terminates. Similarly, the memory of 4040 bytes allocated for the local variables of main() is released when the program terminates.

> If the stack has not enough memory to store the data of a function, the execution of the program would terminate abnormally and the message "Stack overflow" may appear.

This situation may occur when a function allocates large blocks of memory and calls other nested functions with considerable memory needs as well. For example, a recursive function that calls itself many times may cause the exhaustion of the available stack memory.

# Dynamic Memory Allocation

In dynamic allocation, the memory is allocated from the heap during program execution. Unlike static allocation, its size can be dynamically specified. Furthermore, this size may dynamically shrink or grow according to the program's needs. Typically, the default stack size is not very large. For example, the following program might not run because of unavailable stack memory:

```
#include <stdio.h>
int main(void)
{
    int arr[1000000]; /* Static allocation. */
    return 0;
}
```