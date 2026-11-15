
To illustrate, assume that we want to dynamically allocate memory to store a double array named x containing npts elements. (In this example, we give a value to npts, but it could be computed by other statements or read from the keyboard or a data file.) To specify the desired allocation, we could use either of the following sets of statements:

```
Solution 1
/* Declare variables. */
int npts = 500;
double *x;
...
/* Dynamically allocate memory. */
x = (double *)malloc(npts*sizeof(double));
```

```
Solution 2
/* Declare variables. */
int npts = 500;
double *x;
...
/* Dynamically allocate memory. */
x = (double *)calloc(npts,sizeof(double));
```

If the calloc function is used, then the memory values will also be initialized to zero. With either of these solutions, we should compare the value of x to the constant NULL. This will make sure that the memory was allocated, as shown in the following statement:

```
if (x == NULL)
    printf("Memory requested not available. \n");
```

After we have determined that the memory has been allocated, references to the array x, such as x[k], are valid in the program.

To release memory that has been dynamically allocated, use the free function, which has the following prototype:

```
void free(void *ptr);
```

Thus, the memory allocated to array x is released with this statement: free(x);

In general, you should free dynamically allocated memory when it is no longer needed. Then it becomes available for possible use with another dynamic allocation.

The realloc function can be used to change the size of the memory requested by a calloc, malloc, or previously executed realloc function. Its prototype statement is

```
void *realloc(void *ptr,size_t size);
```

If ptr contains the value NULL, this function operates like the malloc function. If ptr contains a value returned earlier in a program by a calloc, malloc, or previously executed realloc function, then the size of the corresponding memory allocation is changed to the new size requested. If the new size is larger, the values of the newly allocated space are undetermined. If the new size is smaller, the values in the new size are unchanged. If the additional space cannot be allocated, the original space is unchanged and the function returns a value of NULL.

With the use of dynamic memory allocations and dynamic memory allocation releases, a program can be designed to operate with a minimal amount of memory reserved at any time during its execution. On systems that run multiple programs at the same time, the use of dynamic memory allocation and dynamic memory release may allow more programs to run simultaneously.

The next program allows you to determine the maximum amount of contiguous memory that can be dynamically allocated during its execution. This maximum amount of memory available is generally a function of the other users on the system and the other software that is stored on the system; thus, you may get different results when you run the program on different systems and at different times. Here is the program:

```
/*------------------------------------------*/
/* Program chapter6_8                         */
/*                                          */
/* This program determines the maximum contiguous */
/* memory allocation that can be reserved during a */
/* specific program execution.                */
/*                                          */
#include <stdio.h>
#include <stdlib.h>
#define UNIT 1000000

int main(void)
{
    /* Declare and initialize variables.     */
    int k=1, *ptr;

    /* Find maximum amount of contiguous memory */
    /* available in units of millions of integers. */
    ptr = (int *)malloc(UNIT*sizeof(int));
    while (ptr != NULL)
    {
        free(ptr);
        k++;
        ptr = (int *)malloc(k*UNIT*sizeof(int));
    }

    /* Print maximum amount of memory available. */
    printf("Maximum contiguous memory available: \n");
    printf("%d integers \n",(k-1)*UNIT);

    /* Exit program.     */
    return 0;
}
/*------------------------------------------*/
```

A typical output for this program using a personal computer is the following:

Maximum contiguous memory available:
31000000 integers

## MODIFY!

Modify program chapter6_8 such that it determines the number of thousands of contiguous values that can be stored for the data types indicated in the following:

- 1. long integers, 2. doubles, and 3. long doubles.

In the previous section, we developed a program that read a set of seismic data from a data file and determined possible seismic event locations within the data. The program used a symbolic constant MAX_SIZE to allocate an array to store the data. If the number of points in the data file exceeded MAX_SIZE, then the program terminated with an error message. In the following, we present statements that use dynamic memory allocation so that the maximum array size does not have to be allocated when the program is compiled (instead, the array memory is dynamically allocated based on the size of the seismic data file):

```
/*
 * Program chapter6_5mod
 *
 * This program reads a seismic data file and then
 * determines the times of possible seismic events.
 * Dynamic memory allocation is used.
 */
#include <stdio.h>
#define FILENAME "seismic1.txt"
#define THRESHOLD 1.5

int main(void)
{
    /* Declare variables and function prototypes. */
    int k, npts, short_window, long_window;
    double sensor, time_incr, short_power,
           long_power, ratio;

    FILE *file_ptr;
    double power_w(double *ptr,int n);

    /* Read data header and allocate memory. */
    file_ptr = fopen(FILENAME,"r");
    if (file_ptr == NULL)
        printf("Error opening input file. \n");
    else
    {
        fscanf(file_ptr,"%d %lf",&npts,&time_incr);
        sensor = (double *)malloc(npts*sizeof(double));
        if (sensor == NULL)
            printf("Not enough memory available. \n");
        else
            (no changes in the remainder of program chapter6_5 on page 312)
}
```

## 6.9 A Quicksort Algorithm*

### Quicksort

### Pivot value

In this section, a quicksort algorithm is implemented with a recursive function (see Section 4.8) that uses pointers as function parameters.

The quicksort algorithm selects a value, called a pivot value, and then separates the rest of the values into two groups—one group containing values less than the pivot value and one group containing values greater than the pivot value. For our purposes, we will select the group value to be the first element in the list, but the midpoint of the list is also often used as the pivot value. When this separation is done, the correct position in the list for the pivot value is determined; it goes between the two groups of values. Since the values in the two groups are not necessarily in the correct order, we take the group of smaller values and select a new pivot value. This group is separated into two new groups of values—ones smaller than the new pivot value and ones larger than the new pivot value. This process continues until we eventually have a group of smaller values that contains no values, one value, or two values. If this group contains two values, their order is switched if necessary, and then the original group of values smaller than the original pivot value are in order. We repeat this process with the original group of values that are larger than the original pivot. When these are in order, the entire list is in order. This algorithm can be described recursively because each step is defined in terms of a similar process with a smaller group of values, and because it has a stopping point that is encountered when the group of values has two or fewer values. A hand example follows:

```
Original list:
4   10   3   6   -1   0   2   5
Separate into groups of values smaller and larger than the pivot value:
[3  -1   0   2]   4   [10   6   5]
Separate each remaining group into groups of values smaller and larger than the pivot value of each group:
[-1   0   2]   3   4   [6   5]   10
Separate each remaining group into groups of values smaller and larger than the pivot of each group:
-1   [0   2]   3   4   5   6   10
Separate each remaining group into groups of values smaller and larger than the pivot of each group:
-1   0   2   3   4   5   6   10
```

The implementation of the quicksort algorithm that we present references an additional function named separate. This function switches values in the array that it receives such that the pivot value is correctly positioned in the position referenced by break_pt. All values less than the pivot value are to the left in the array (if we visualize the array as a row), and all values greater than the pivot value are to the right. Then, the quicksort function is recursively called using a statement which specifies that a total of break_pt values, starting with x[0], should be sorted:

```
quicksort(x, break_pt);
```
