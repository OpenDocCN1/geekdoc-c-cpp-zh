that array, &array and &array[0] have the same value. This program’s output is system dependent, but the addresses are always identical for each program execution on a particular computer.

```
```c
// Fig06_10.c
// Array name is the same as the address of the array's first element.
#include <stdio.h>

// function main begins program execution
int main(void) {
   char array[5] = ""; // define an array of size 5

   printf("    array = %p\n&array[0] = %p\n&array = %p\n",
          array, &array[0], &array);
}
```
```

```
```
array = 0031F930
&array[0] = 0031F930
&array = 0031F930
```
```

Fig. 6.10 | Array name is the same as the address of the array's first element.

Passing arrays by reference makes sense for performance reasons. If arrays were passed by value, a copy of each element would be passed. For large, frequently passed arrays, this would be time-consuming and would consume storage for the copies of the arrays. It’s possible to pass an array by value (by placing it in a struct, as we explain in Chapter 10, Structures, Unions, Bit Manipulation and Enumerations).

# ### Passing Individual Array Elements

Although entire arrays are passed by reference, individual array elements are passed by value, exactly as any other variable. Single pieces of data, such as individual ints, floats and chars, are called scalars. To pass an array element to a function, use the subscripted array name as an argument in the function call. In Chapter 7, we show how to pass scalars (i.e., individual variables and array elements) to functions by reference.

# ### Array Parameters

For a function to receive an array through a function call, the function’s parameter list must expect an array. The function header for function `modifyArray` (from earlier in this section) can be written as

```
```c
void modifyArray(int b[], size_t size)
```
```

indicating that `modifyArray` expects to receive an int array in parameter b and the array’s number of elements in parameter size. The array’s number of elements is not required in the array parameter’s brackets. If it’s included, the compiler checks that it’s greater than zero, then ignores it—specifying a negative value is a compilation error. When the called function uses the array name b, it will be referring to the caller’s original array. So, in the function call: