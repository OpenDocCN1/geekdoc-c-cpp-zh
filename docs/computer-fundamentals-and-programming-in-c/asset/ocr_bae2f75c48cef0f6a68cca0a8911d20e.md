Here, the variable size array declaration, e.g.,

```
```c
double x[N], y[N];
```
```

is used where N is an integer variable. This kind of declaration is illegal in C and results in a compile-time error.

It is sometimes convenient to define an array size in terms of a symbolic constant, rather than a fixed integer quantity. This makes it easier to modify a program that utilizes an array, since all references to the maximum array size can be altered by simply changing the value of the symbolic constant. This approach is used in many of the sample programs given in this book. Consider the following sample program, which uses this approach.

```
```c
/* Define a symbolic constant for the size of
   the array */
#include <stdio.h>
#define N 100
int main()
{
    double x[N], y[N];
    ...
    return 0;
}
```
```

![](bbox=[0.2, 0.268, 0.37, 0.315])

![](bbox=[0.19, 0.365, 0.36, 0.412])

It is a good programming practice to define the size of an array as a symbolic constant.

Hence, it may be observed that a literal number or a previously declared #defined symbolic constant must be used in an array declaration for the size of the array. No variables are allowed for the size of the array.

Since the number of array elements can also be given by an expression, the declarations depicted below can be used.

```
```c
int x[N+1];
double y[M*5*N];
```
```

However, the C compiler must be able to evaluate the expression, which implies that all components of the expression must be available for evaluation of the expression when the program is compiled—there must be no unknowns. This means that the expression must be composed of constants. In the preceding examples, identifiers consisting of capital letters have been used, which is the convention for symbols defined with #define directives.

Thus the following expressions accessing elements of array arr are valid.

```
```c
/* Give N a value so that the examples are concrete! */
#define N 20
int i = 1, j = 3, k = 2;
float arr[N];

arr[0]
arr[3]
arr[9]
arr[i*j*k]/* given values of i,j,k evaluates i*j*k to 5 */
```
```

![](bbox=[0.21, 0.72, 0.37, 0.77])

```
```c
arr[N-10]
arr[N-1]
```
```

The following array references are not valid.

```
```c
arr[-1]
arr[N-2]
arr[N+20]
arr[N]
```
```

In the previous example, arr[N-1] is the cause of many problems for new C programmers. It must be remembered that C array indices start at 0. Thus for an array with N elements, the index of the last element is N-1. It may be of help to think of the array index as an offset from the beginning of the array, so that the first element is at offset 0 from the beginning, is arr[0] and the last, at offset N-1, must be arr[N-1].

Thus, expressions such as arr[N] are happily accepted by the compiler. (C compilers usually make the assumption that programmers know what they are doing.) The results of running such programs are entirely unpredictable, since the space at the end of the array may have arbitrary data in it. The results from a program may even vary from one run to another, as the memory space in which the compiler assumes the (N+1)th object to be stored may well have been allocated to some other object.

+   **Note**
+   
+   - In C, arrays are of two types: one-dimensional and multidimensional.
+   - An array must be declared with three attributes: type of data it can hold, the number of data it can hold(size), and an identifier(name) before it is used.
+   - The array size must be a positive integer number or an expression that evaluates to a positive integer number that must be specified at the time of declaration with the exception that it may be unspecified while initializing the array.
+   - In C, the array index starts at 0 and ends at (size-1) and provides the means of accessing and modifying the specific values in the array.
+   - C never checks whether the array index is valid—either at compile time or when the program is running.

# ### 11.2.2 Initializing Integer Arrays

Variables can be assigned values during declaration like the following example.

```
```c
int x = 7;
```
```

Arrays can be initialized in the same manner. However, since an array has multiple elements, braces are used to denote the entire array of values and commas are used to separate the individual values assigned to the elements in the array initialization statements as shown.

```
```c
(a) int A[10] = {9, 8, 7, 6, 5, 4, 3, 2, 1, 0};
```
```