# 404 Introduction to C++

the array remains fixed; if we need to store grades for more students, we cannot change it during program execution. If the students proved to be less than 1000, memory is wasted. The only way to change the length of the array is to modify the program and compile it again.

Let's discuss briefly happens when a function is called. The compiler allocates memory in the stack to store the function's data. As said, system registers may be used; for simplicity, we assume that the allocation occurs in the stack. For example, if the function returns a value, accepts parameters, and uses local variables, the compiler allocates memory to store:

+   a. The values of the parameters.
b. The local variables.
c. The return value.
d. The address of the next statement to be executed, when the function terminates.

When the function terminates, the following actions take place:

+   a. If the return value is assigned to a variable, it is extracted from the stack and stored into that variable.
b. The address of the next statement is extracted from the stack and the execution of the program continues with that statement.
c. The memory allocated to the function's data is released (except that of the static variables).

For example, in the following program, when test() the compiler allocates 202xsizeof(int) bytes in the stack to store the values of i, j, and arr elements:

```
#include <iostream> // Example 14.1

void test(int i, int, int j);

int main()
{
    float a[1000], b[10];
    test(10, 20);
    return 0;
}

void test(int i, int, j)
{
    int arr[200];
}
```

This memory is automatically released when test() terminates. Similarly, the memory of 1010*sizeof(float) bytes allocated for the local variables of main() is released when the program terminates.

> If the stack has not enough memory to store the data of a function, the execution of the program would terminate normally and the stack overflow may appear.

This situation may occur when a function allocates large blocks of memory and calls other functions with considerable memory needs as well. For example, a recursive function that calls itself times may cause the exhaustion of the available stack memory.

![](bbox=[0.085, 0.825, 0.15, 0.855])