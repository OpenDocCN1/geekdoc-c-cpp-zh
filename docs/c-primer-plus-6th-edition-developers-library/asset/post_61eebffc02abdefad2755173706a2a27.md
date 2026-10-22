
The functions registered by atexit() should, like sign_off() and too_bad(), be type void functions taking no arguments. Typically, they would perform housekeeping tasks, such as updating a program-monitoring file or resetting environmental variables.

Note that sign_off() is called even when exit() is not called explicitly; that’s because exit() is called implicitly when main() terminates.

## Using exit()

After exit() executes the functions specified by atexit(), it does some tidying of its own. It flushes all output streams, closes all open streams, and closes temporary files created by calls to the standard I/O function tmpfile(). Then exit() returns control to the host environment and, if possible, reports a termination status to the environment. Traditionally, Unix programs have used 0 to indicate successful termination and nonzero to report failure. Unix return codes don’t necessarily work with all systems, so ANSI C defined a macro called EXIT_FAILURE that can be used portably to indicate failure. Similarly, it defined EXIT_SUCCESS to indicate success, but exit() also accepts 0 for that purpose. Under ANSI C, using the exit() function in a nonrecursive main() function is equivalent to using the keyword return. However, exit() also terminates programs when used in functions other than main().

## The qsort() Function

The “quick sort” method is one of the most effective sorting algorithms, particularly for larger arrays. Developed by C.A.R. Hoare in 1962, it partitions arrays into ever smaller sizes until the element level is reached. First, the array is divided into two parts, with every value in one partition being less than every value in the other partition. This process continues until the array is fully sorted.

The name for the C implementation of the quick sort algorithm is qsort(). The qsort() function sorts an array of data objects. It has the following ANSI prototype:

```c
void qsort (void *base, size_t nmemb, size_t size,
    int (*compar)(const void *, const void *));
```

The first argument is a pointer to the beginning of the array to be sorted. ANSI C permits any data pointer type to be typecast to a pointer-to-void, thus permitting the first actual argument to qsort() to refer to any kind of array.

The second argument is the number of items to be sorted. The prototype converts this value to type size_t. As you may recall from several previous mentions, size_t is the integer type returned by the sizeof operator and is defined in the standard header files.

Because qsort() converts its first argument to a void pointer, qsort() loses track of how big each array element is. To compensate, you must tell qsort() explicitly the size of the data object. That’s what the third argument is for. For example, if you are sorting an array of type double, you would use sizeof(double) for this argument.

Finally, qsort() requires a pointer to the function to be used to determine the sorting order. The comparison function should take two arguments: pointers to the two items being compared. It should return a positive integer if the first item should follow the second item, zero if the two items are the same, and a negative integer if the second item should follow the first. The qsort() function will use this function, passing it pointer values that it calculates from the other information given to it.

The form the comparison function must take is set forth in the qsort() prototype for the final argument:

```c
int (*compar)(const void *, const void *)
```

This states that the final argument is a pointer to a function that returns an int and that takes two arguments, each of which is a pointer to type const void. These two pointers point to the items being compared.

Listing 16.17 and the discussion following it illustrate how to define a comparison function and how to use qsort(). The program creates an array of random floating-point values and sorts the array.

### Listing 16.17 The qsorter.c Program

```c
/* qsorter.c -- using qsort to sort groups of numbers */
#include <stdio.h>
#include <stdlib.h>

#define NUM 40
void fillarray(double ar[], int n);
void showarray(const double ar[], int n);
int mycomp(const void * p1, const void * p2);

int main(void)
{
    double vals[NUM];
    fillarray(vals, NUM);
    puts("Random list:");
    showarray(vals, NUM);
    qsort(vals, NUM, sizeof(double), mycomp);
    puts("\nSorted list:");
    showarray(vals, NUM);
    return 0;
}

void fillarray(double ar[], int n)
{
    int index;

    for (index = 0; index < n; index++)
        ar[index] = (double)rand()/((double) rand() + 0.1);
}

void showarray(const double ar[], int n)
{
    int index;

    for (index = 0; index < n; index++)
    {
        printf("%9.4f ", ar[index]);
        if (index % 6 == 5)
            putchar('\n');
    }
    if (index % 6 != 0)
        putchar('\n');
}

/* sort by increasing value */
int mycomp(const void * p1, const void * p2)
{
    /* need to use pointers to double to access values  */
    const double * a1 = (const double *) p1;
    const double * a2 = (const double *) p2;

    if (*a1 < *a2)
        return -1;
    else if (*a1 == *a2)
        return 0;
    else
        return 1;
}
```

Here is a sample run:

```text
Random list:
    0.0001    1.6475    2.4332    0.0693    0.7268    0.7383
   24.0357    0.1009   87.1828    5.7361    0.6079    0.6330
    1.6058    0.1406    0.5933    1.1943    5.5295    2.2426
    0.8364    2.7127    0.2514    0.9593    8.9635    0.7139
    0.6249    1.6044    0.8649    2.1577    0.5420   15.0123
    1.7931    1.6183    1.9973    2.9333   12.8512    1.3034
    0.3032    1.1406   18.7880    0.9887

Sorted list:
    0.0001    0.0693    0.1009    0.1406    0.2514    0.3032
    0.5420    0.5933    0.6079    0.6249    0.6330    0.7139
    0.7268    0.7383    0.8364    0.8649    0.9593    0.9887
    1.1406    1.1943    1.3034    1.6044    1.6058    1.6183
    1.6475    1.7931    1.9973    2.1577    2.2426    2.4332
    2.7127    2.9333    5.5295    5.7361    8.9635    12.8512
    15.0123   18.7880   24.0357   87.1828
```

Let’s look at two main areas: the use of qsort() and the definition of mycomp().

### Using qsort()

The qsort() function sorts an array of data objects. The ANSI prototype, again, is this:

```c
void qsort (void *base, size_t nmemb, size_t size,
    int (*compar)(const void *, const void *));
```

The first argument is a pointer to the beginning of the array to be sorted. In this program, the actual argument is vals, the name of an array of double, hence a pointer to the first element of the array. The ANSI prototype causes the vals argument to be typecast to type pointer-to-void. That’s because ANSI C permits any data pointer type to be typecast to a pointer-to-void, thus permitting the first actual argument to qsort() to refer to any kind of array.

The second argument is the number of items to be sorted. In Listing 16.17, it is NUM, the number of array elements. The prototype converts this value to type size_t.

The third argument is the size of each element—sizeof(double), in this case.

The final argument is mycomp, the address of the function to be used for comparing elements.

### Defining mycomp()

As mentioned before, the qsort() prototype mandates the form of the comparison function:

```c
int (*compar)(const void *, const void *)
```

This states that the final argument is a pointer to a function that returns an int and that takes two arguments, each of which is a pointer to type const void. We made the prototype for the mycomp() function agree with this prototype:

```c
int mycomp(const void * p1, const void * p2);
```

Remember that the name of the function is a pointer to the function when used as an argument, so mycomp matches the compar prototype.

The qsort() function passes the addresses of the two elements to be compared to the comparison function. In this program, then, p1 and p2 are assigned the addresses of two type double values to be compared. Note that the first argument to qsort() refers to the whole array, and the two arguments in the comparison function refer to two elements in the array. There is a problem. To compare the pointed-to values, you need to dereference a pointer. Because the values are type double, you need to dereference a pointer to type double. However, qsort() requires pointers to type void. The way to get around this problem is to declare pointers of the proper type inside the function and initialize them to the values passed as arguments:
