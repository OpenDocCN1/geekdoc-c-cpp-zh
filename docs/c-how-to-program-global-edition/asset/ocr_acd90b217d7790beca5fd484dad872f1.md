sion specifier for printing addresses. The %p conversion specifier normally outputs addresses as hexadecimal numbers, but this is compiler dependent. Hexadecimal (base 16) numbers consist of the digits 0 through 9 and the letters A through F (these letters are the hexadecimal equivalents of the decimal numbers 10–15). Appendix C provides an in-depth discussion of the relationships among binary (base 2), octal (base 8), decimal (base 10; standard integers) and hexadecimal integers. The output shows that array, &array and &array[0] have the same value, namely 0031F930. The output of this program is system dependent, but the addresses are always identical for a particular execution of this program on a particular computer.

![](bbox=[0.14, 0.278, 0.204, 0.326])

# **Performance Tip 6.3**

*Passing arrays by reference makes sense for performance reasons. If arrays were passed by value, a copy of each element would be passed. For large, frequently passed arrays, this would be time consuming and would consume storage for the copies of the arrays.*

```
```c
// Fig. 6.12: fig06_12.c
// Array name is the same as the address of the array's first element.
#include <stdio.h>

// function main begins program execution
int main(void)
{
    char array[5]; // define an array of size 5

    printf("    array = %p\n&array[0] = %p\n    &array = %p\n",
           array, &array[0], &array);
}
```
```

```
```text
    array = 0031F930
&array[0] = 0031F930
    &array = 0031F930
```
```

**Fig. 6.12** | Array name is the same as the address of the array’s first element.

![](bbox=[0.14, 0.736, 0.204, 0.784])

# **Software Engineering Observation 6.2**

*It’s possible to pass an array by value (by placing it in a struct as we explain in Chapter 10, C Structures, Unions, Bit Manipulation and Enumerations).*

Although entire arrays are passed by reference, individual array elements are passed by value exactly as simple variables are. Such simple pieces of data (such as individual ints, floats and chars) are called scalars. To pass an element of an array to a function, use the indexed name of the array element as an argument in the function call. In Chapter 7, we show how to pass scalars (i.e., individual variables and array elements) to functions by reference.

For a function to receive an array through a function call, the function’s parameter list must specify that an array will be received. For example, the function header for function modifyArray (that we called earlier in this section) might be written as

```
```c
void modifyArray(int b[], size_t size)
```
```