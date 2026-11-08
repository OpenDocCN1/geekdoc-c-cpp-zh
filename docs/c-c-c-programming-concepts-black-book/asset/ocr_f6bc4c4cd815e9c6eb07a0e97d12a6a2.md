# Exploring Array of Function Pointers

An array, whose members are pointers to a function, is known as array of function pointers. An array of function pointers is not much different from array of pointers. The only difference is that instead of pointers, an array contains function pointers. An array of function pointers provides the flexibility to select one of the functions using a subscript of an array. Listing 4.18 shows the usage of an array of function pointers:

Listing 4.18: Showing the Code to use an Array of Function Pointers

```
# include<stdio.h>
#include<string.h>
int Add(int,int);
int Sub(int,int);
int Mul(int,int);
typedef int(*func_ptr)(int,int);
func_ptr arr_func_ptr[3];
int dooperation(int, int, int (*func_ptr)(int, int));
int main()
{
    int varA = 20;
    int varB = 10;
    arr_func_ptr[0] = &Add;
    arr_func_ptr[1] = &Sub;
    arr_func_ptr[2] = &Mul;
    printf("\n Addition       : [%d] ",dooperation(varA , varB ,arr_func_ptr[0]));
    printf("\n subtraction : [%d] ",dooperation(varA , varB ,arr_func_ptr[1]));
    printf("\n Multiply        : [%d] ",dooperation(varA , varB ,arr_func_ptr[2]));
    getch();
    return 0;
}
int dooperation(int varA, int varB, int (*func_ptr)(int, int))
{
    return (func_ptr(varA, varB));
}
int Add(int varA ,int varB) { return varA + varB; }
int Sub(int varA ,int varB) { return varA - varB; }
int Mul(int varA ,int varB) { return varA * varB; }
```

In Listing 4.18, we have declared an array of function pointers called arr_func_ptr. This function pointer points to a function that takes two integers as its arguments and returns an integer. We have manually stored the addresses of various functions in different cells of the array. The wrapper function doOperation() is used to invoke the correct function with its argument, thereby, giving the desired result.

In the next section, let’s learn about callbacks.

# Callbacks

A callback is nothing but a function that is called with the help of a function pointer. The main advantage of using a callback is the detachment between the caller function and the called function. In other words, the caller function need not care about to whom the actual call is being made. To understand the concept of callbacks, let’s take an example of various sorting techniques, such as Bubble Sort, Quick Sort, and Selection. Irrespective of the sorting techniques, a generic scheme can be devised with the help of callbacks to perform the comparison between two values. By doing this, we can keep the comparison logic same and reuse the module from different sorting techniques. Another usage of callbacks comes from event notifications. Let’s assume that we have a timer tied to an application and each time the timer expires, the application needs to be notified. However, the implementation of the timer is made in such a way that it does not know anything