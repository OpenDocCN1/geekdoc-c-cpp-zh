```
```
main()
{
   /* Initialize variables */
   int i_first=10, i_second=20;

   /* Print old values */
   printf("\nthe old values of first and second are %d and %d", i_first,
         i_second);

   /* Function call to exchange for swapping values of two variables*/
   exchange(&i_first,&i_second);

   /* Print new values */
   printf("\nthe new values of first and second are %d and %d", i_first,
         i_second);
   return;
}
/* End of function main */

/* Beginning of function exchange */
void exchange(int *i_first, int *i_second)
{
   int i_temp;
   i_temp=*i_first;
   *i_first=*i_second;
   *i_second=i_temp;
}
/* End of function exchange */
```
```

**Output:**

The old values of first and second are 10 and 20
The new values of first and second are 20 and 10

Program 13 calls a function exchange in the main program. The parameters of a function exchange are pointers. These addresses are received by the pointers i_first and i_second. Now, when the values of i_first and i_second are manipulated, the new values are written to the memory addresses directly. Thus, when a function is returned and the values of i_first and i_second are displayed again in calling function, new values are displayed on the screen.

# ## Functions Returning Pointer

We have seen that functions can accept addresses as parameters and return multiple values with the help of pointers. Since pointers are data type in C, functions can also return a pointer. Let us write a program to add two numbers. The result of addition will be returned as pointer to a variable. Program 14 illustrates the use of function returning a pointer.

# ### Program 14

```
```c
/* Program to illustrate function returning pointer*/
#include<stdio.h>

/* Function prototype*/
```
```