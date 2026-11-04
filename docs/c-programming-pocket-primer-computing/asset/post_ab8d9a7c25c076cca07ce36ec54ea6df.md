
int floats1[] = {1.0,2.0,3.0,4.0,5.0};
float *ptr2 = floats1;
int fsize1 = sizeof(floats1)/sizeof(float);

double doubles1[] = {1.0,2.0,3.0,4.0,5.0};
double *ptr3 = doubles1;
int dsize1 = sizeof(doubles1)/sizeof(double);

printf("The ints1 array:\n");
for(int i=0; i<isize1; i++)
{
    printf("%d ", *(ptr1+i));
}
printf("\n");

for(int i=0; i<isize1; i++)
{
    printf("%f ", *(ptr1+i));
}
printf("\n");

printf("The floats1 array:\n");
for(int i=0; i<fsize1; i++)
{
    printf("%d ", *(ptr2+i));
}
printf("\n");

for(int i=0; i<fsize1; i++)
{
    printf("%f ", *(ptr2+i));
}
printf("\n");

printf("The doubles1 array:\n");
for(int i=0; i<dsize1; i++)
{
    printf("%d ", *(ptr3+i));
}
}
    printf("\n");

    for(int i=0; i<dsize1; i++)
    {
        printf("%f ", *(ptr3+i));
    }
    printf("\n");

    return 0;
}
```

Listing 6.11 contains three arrays `ints1`, `floats1`, and `doubles1` that contain the same set of decimal values, along with the pointers `ptr1`, `ptr2`, and `ptr3` that "point" to each of these arrays. The next portion of Listing 6.11 contains three "pairs" of `for` loops, each of which displays the contents one of the arrays. For instance, the first pair of loops displays the contents of the `ints1` array in two ways: the first loop contains a `printf()` statement with the `%d` format and the second loop uses a `printf()` statement with the `%f` format.

Look closely at the declarations for the three arrays and the way the values in the arrays are printed: are the results consistent with your predictions? The output from launching the code in Listing 6.11 is here:

```
The ints1 array:
1 2 3 4 5
0.000000 0.000000 0.000000 0.000000 0.000000
The floats1 array:
1 2 3 4 5
0.000000 0.000000 0.000000 0.000000 0.000000
The doubles1 array:
1 2 3 4 5
1.000000 2.000000 3.000000 4.000000 5.000000
```

## "REVERSING" AN ARRAY OF NUMBERS

The code sample in this section for “reversing” an array of numbers does not work because of an intentional bug (can you find the bug and fix it?). Listing 6.12 displays the contents of ReverseArrayNums1.c that seems to reverse an array of numbers using a pointer.

### LISTING 6.12: ReverseArrayNums1.c

```
#include <stdio.h>

int main()
{
    // int array with 6 elements
    int arr1[6] = {1,2,3,4,5,6};
    int *ptr1, count=6;

    printf("Initial: ");
    for(int i=0; i<count; i++)
    {
        printf("%d ",arr1[i]);
    }
    printf("\n");

    for(int i=0; i<count/2; i++)
    {
        ptr1 = &arr1[i];
        printf("ptr = %d ", *ptr1);

        arr1[i] = arr1[count-i-1];
        printf("left = %d ", arr1[i]);

        arr1[count-i-1] = *ptr1;
        printf("right = %d\n", *ptr1);
    }
```

```
printf("Reversed: ");
for(int i=0; i<count; i++)
{
    printf("%d ",arr1[i]);
}
printf("\n");

return 0;
}
```

Listing 6.12 contains a main() function that initializes the array arr1 with a set of integers, and then declares the integer pointer ptr1 and the integer count (whose initial value is 6).

The next portion of the main() function contains a loop that iterates through the elements of the array arr1 and displays the values of those elements. The second loop iterates through the first half of the array arr1 and “swaps” each element with its counterpart in the right half of the array arr1.

The logic is very similar to the code that checks for palindromes, with code that uses the pointer ptr1 as a temporary storage location in order to switch the two values.

As you can see in the code, the “counterpart” of the element arr1[i] is arr1[count-i-1]. The final loop iterates through the elements of the array arr1 (which have been reversed). The output from launching the code in Listing 6.12 is here:

```
Initial: 1 2 3 4 5 6
ptr = 1 left = 6 right = 6
ptr = 2 left = 5 right = 5
ptr = 3 left = 4 right = 4
Reversed: 6 5 4 4 5 6
```

The loop in Listing 6.12 attempts to swap by executing this code sequence: a = b; b = a; a = b; which obviously does not perform a swap: it simply assigns b to a. The solution involves performing a *correct* swap. The purpose of this code sample is to show you how easy it is to write buggy C code that looks correct.

## MEMORY ALLOCATION FUNCTIONS IN C

The C programming language supports several functions that enable you to dynamically allocate (and free) memory in a C program:

- malloc()
- calloc()
- realloc()
- free()

The malloc() function allocates a block memory in C programs, which is very useful when you define custom structures (as discussed in chapter 6).

The calloc() function allocates a block of memory (just like the malloc() function) and also initializes the allocated memory to zero.

The realloc() function resizes a memory block that was allocated by malloc() or calloc(). If there is sufficient room after the memory block, or if the block is shrinking, it may be possible to do the reallocation in place. If the memory block needs to be reallocated in a new location, the existing data will be copied to the new block and the old block will be freed.

The free() function has the opposite purpose: it frees the memory that was allocated by the functions malloc(), calloc(), realloc(). Failure to invoke the free() function after dynamically allocating memory causes memory leaks.

Use the `malloc()` function to copy strings and the `strncpy()` function to specify the number of characters that you want to copy, or use the `strdup()` function to allocate memory and copy an entire string in one operation.

The next few sections contain code samples that illustrate how to dynamically allocate memory in C.

## THE BUILT-IN MALLOC() C FUNCTION

Listing 6.13 displays the contents of CopyFunction2.c that illustrates how to use the malloc() function and the strncpy() function.

### LISTING 6.13: CopyFunction2.c

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
   char *src = "This is one line of text";
   char *dest;
   int len;
   len = strlen(src);

   dest = (char *)malloc(sizeof(src));

   // fill up 'dest'
   strncpy(dest, src, len);

   // not required because 'strncpy' adds a null terminator:
   //dest[len-1] = '\0';
```

without ever freeing that memory, then you will have what is commonly called a "memory leak."

## JAGGED ARRAYS

This section contains a C program that illustrates how to work with jagged arrays, which are arrays that contain elements of different lengths. For example, you can define an array of names, where each name is a string of a different length.

Listing 6.14 displays the contents of JaggedArray1.c that shows you how to calculate the sum of the entries in a multi-dimensional array.

```
**LISTING 6.14: JaggedArray1.c**

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
   int rowLengths[] = {6,4,3,5};
   int *jagged[4];

   for (int i = 0; i < 4; ++i)
   {
      jagged[i] = (int *)malloc(sizeof(int) * rowLengths[i]);
   }

   for (int i=0; i<4; ++i)
   {
      for (int j=0; j<rowLengths[i]; ++j)
      {
         jagged[i][j] = i + j + i*i;
         printf("element (%d,%d) = %d\n", i, j, jagged[i][j]);
      }
```
```

```
}
}
```

Listing 6.14 initializes the integer array `rowLengths` with the lengths of 4 rows. Next, the variable `jagged` is declared as a pointer to an array of 4 integer-valued pointers.

The first loop iterates through the 4 rows of `jagged`, and uses the built-in `malloc()` C function to allocate memory for the number of integers that are specified in the `rowLengths` array. For instance, `jagged[0]` is initialized as a pointer to 6 integers, whereas `jagged[1]` is initialized as a pointer to 4 integers.

The second loop is a nested loop that initializes the value of the “cell” at position (i,j) with the value i + j + i*j, and then immediately displays that value via the `printf()` function. Launch the code in Listing 6.14 and you will see the following output:

```
element (0,0) = 0
element (0,1) = 1
element (0,2) = 2
element (0,3) = 3
element (0,4) = 4
element (0,5) = 5
element (1,0) = 1
element (1,1) = 3
element (1,2) = 5
element (1,3) = 7
element (2,0) = 2
element (2,1) = 5
element (2,2) = 8
element (3,0) = 3
element (3,1) = 7
element (3,2) = 11
element (3,3) = 15
element (3,4) = 19
```
