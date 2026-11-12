# Want addresses?

As with index values, the value added to `a` represents an offset from the memory address value that `a` represents. The addition results in a new memory address. Don't different data types require different amounts of memory? Yes, but adding one to a pointer will advance to the next element in the array based on the type of the array. In the case of integer data on our server the addition of one will be an increment of four bytes.

```
void printArray(int*);

int main(void)
{
   int a[5] = { 2, 4, 5, 3, 1};

   printf("Array a address: %p\n", a);

   printArray(a);

   return(0);
}
```

![](bbox=[0.43, 0.19, 0.82, 0.43])

```
void printArray(int *y)
{
   int i;

   printf("Array y address: %p\n", y);

   for(i = 0; i < 5; i++)
   {
      printf("&y[%d] = %p\n", i, y + i);
   }
}
```

Output Generated:
Array a address: 0x7ffd003f7680
Array y address: 0x7ffd003f7680
&y[0] = 0x7ffd003f7680
&y[1] = 0x7ffd003f7684
&y[2] = 0x7ffd003f7688
&y[3] = 0x7ffd003f768c
&y[4] = 0x7ffd003f7690

# Memory Allocation Functions

The declaration of the capacity of an array before the program is ever compiled has several limitations that you may have already considered. First, we may not reserve enough memory for the problem. Second, we may reserve too much limiting that which remains for other data. Our venture into dynamic memory allocation will improve our ability to request exactly the memory needed for the problem.

To dynamically allocate memory we will make use of a predefined function called malloc that is found in the stdlib.h library.

+   * The malloc (m-emory alloc-ation) function will allocate a specified number of bytes of memory. A pointer variable must be used to reference the starting address of the newly allocated memory returned from the malloc function.