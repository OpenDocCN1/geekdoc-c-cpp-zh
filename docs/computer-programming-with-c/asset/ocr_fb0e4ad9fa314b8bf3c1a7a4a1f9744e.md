![](bbox=[0.147, 0.108, 0.855, 0.449])

key point to note is that when an array is passed as an argument, the ‘actual argument’ and the ‘formal argument’ share a **common data space** in the memory and hence any change made to the array by the ‘called’ function is also reflected in the ‘calling’ function (as the array is internally one and the same).

Let us assume that `a` is the array with `n` valid elements, created in the `main()` function containing integers to be sorted in descending order. We can pass this array to the function `sort_desc()` to arrange `n` numbers in descending order as shown in Figure 7.28. Note that `p` is a formal argument created inside the function `sort_desc()` which sorts the array using the sorting algorithm discussed in Chapter 6, section 6.2.5. The array `p` and the array `a` will share the same memory space and hence sorting array `p` is same as sorting array `a`. The changes in the array made by the function `sort_desc()` using `p` will be automatically reflected in the `main()` function as well. Hence, it is not required to have a return statement in the function `sort_desc()` as the results are as such available to `main()`. When the `main()` function prints the array after the `sort_desc()` function is executed it gets the descending order at the output of the program as seen in the code, because the array arranged by `sort_desc()` is same as that of the array used by `main()`.

The return type of function `sort_desc()` is set as void because it is not required to return any value to `main()` as both the functions share the same array space. Given below is the full source code to arrange n numbers in ascending order.

```
```c
#include<stdio.h>
void sort_desc(int[] , int);
void main()
{
```
```