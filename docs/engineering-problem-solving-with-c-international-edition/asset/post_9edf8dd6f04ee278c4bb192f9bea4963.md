
The quicksort function is also recursively called using a statement that specifies that a total of n-break_pt-1 values, starting with x[break_pt+1], should be sorted:

```
quicksort(&x[break_pt+1], n-break_pt-1);
```

Note that the actual argument uses &x[break_pt+1], a reference to the address of x[break_pt+1]. This address reference is necessary because using x[break_pt+1] generates a call-by-value, not a call-by-reference. The quicksort function and the separate function use the switch2 function developed in Section 6.2. Since the quicksort algorithm is a complicated algorithm, a good way to begin is to use the hand example and work through the statements using that data.

/*---------------------------------------------*/
/* Program chapter6_9 */
/* */
/* This program tests the quicksort function. */
/*---------------------------------------------*/
#include <stdio.h>

int main(void)
{
/* Declare and initialize variables. */
int x[8]={4,10,3,6,-1,0,2,6}, npts=8, k;
void quicksort(int w[],int n);
int separate(int y[],int m);
void switch2(int *a,int *b);

/* Sort and print the array. */
printf("Before: ");
for (k=0; k<7; k++)
printf("%d ",x[k]);
printf("\n");
quicksort(x,npts);
printf("After: ");
for (k=0; k<7; k++)
printf("%d ",x[k]);
printf("\n");

/* Exit program. */
return 0;
}

/*---------------------------------------------*/
/* This function implements a quicksort algorithm. */
/*---------------------------------------------*/
void quicksort(int w[],int n)
{
/* Declare variables and function prototypes. */
int break_pt;
int separate(int y[],int m);
void switch2(int *a,int *b);

/* If only two elements, order them correctly. */
if (n == 2)
{
    if (w[0] > w[1])
        switch2(&w[0],&w[1]);
}
else
/* If more than two elements, separate into those */
/* greater than and those less than a breakpoint. */
if (n > 2)
{
    break_pt = separate(w,n);
    quicksort(w,break_pt);
    quicksort(&w[break_pt+1],n-break_pt-1);
}
/* Void return. */
return;
}

/*------------------------------------------------------*/
/* This function reorders the array such that y[0] is   */
/* correctly positioned and the values less than it are */
/* to the right and the values greater are to the left. */
int separate(int y[],int m)
{
    /* Declare variables and function prototypes. */
    int k1=1, k2=1, count=0, pivot;
    void switch2(int *a,int *b);

    /* Separate values into two groups. */
    pivot = y[0];
    while (k1<m && k2<m)
    {
        while ((k1<m) && (y[k1]>pivot))
            k1++;
        while ((k2<m) && (y[k2]<pivot))
            k2++;
        if ((k1<m) && (k2<m))
        {
            switch2(&y[k1],&y[k2]);
            count++;
        }
    }
}

/* Put pivot value in correct position. */
if (count > 0)
    switch2(&y[0],&y[count]);
else
{
    k1 = 0;
    while (((k1<m-1) && (y[k1]>y[k1+1])))
    {
        switch2(&y[k1],&y[k1+1]);
        k1++;
    }
    count = k1;
}
/* Return count. */
return count;
}
/*--------------------------------------------------*/
/* Correct function to switch values in two variables. */
/*--------------------------------------------------*/
void switch2(int *a,int *b)
{
    /* Declare variables. */
    int hold;
    /* Switch values in a and b. */
    hold = *a;
    *a = *b;
    *b = hold;
    /* void return. */
    return;
}
/*--------------------------------------------------*/

The focus of this chapter was the relationship between a pointer and the variable to which it points. Examples were presented that demonstrated how to define pointers and how to initialize them. The valid types of operations that can be performed with pointers were listed, and the precedence relationships for operators were updated to include the address operator and the indirection operator. Examples of pointers used as function parameters and in references to arrays were given. We also presented a group of functions that work with character strings; many of these functions use pointers as function parameters. Finally, we presented the C statements that allow us to do dynamic memory allocation using pointers.

![](img/02c4582f051c5b51776411c92b079035_350_0.png)

## KEY TERMS

- address
- address operator
- byte
- character string
- concatenate
- dereference
- dynamic memory allocation
- indirection
- NULL character
- offset
- pointer
- void pointer

## C STATEMENT SUMMARY

Pointer declaration:

```
int *ptr1;
double a, *ptr_2=&a;
```

Dynamic memory allocation:

```
x = (double *)malloc(npts*sizeof(double));
x = (double *)calloc(npts,sizeof(double));
```

## NOTES

- 1. Choose identifiers for pointers that clearly indicate that the identifiers are associated with pointer variables.
- 2. If a pointer is not initially assigned to a memory location, give it a value of NULL to indicate that it has not yet been assigned.

## DEBUGGING NOTES

- 1. Be sure that a program initializes a variable before using its value in other statements.
- 2. Be sure that a pointer variable is initialized before it is used to reference a value.
- 3. The actual parameter that corresponds to a pointer argument in a function must be an address or a pointer.

## PROBLEMS

### SHORT ANSWER PROBLEMS

### True-False Problems

Indicate whether the following statements are true (T) or false (F).

- 1. Both the address operator and the indirection operator are unary operators. T F
- 2. A pointer provides an indirect means of accessing the value of a particular data item. T F
- 3. A variable must always be declared and initialized before a pointer can point to it. T F
- 4. The memory locations given to dynamic memory space are determined when the program is compiled. T F

### Multiple Choice Problems

Circle the letter for the best answer to complete each statement or for the correct answer of each question.

- 5. A location in memory
- (a) is reserved whenever a variable is declared.
- (b) is reserved when a variable is used in a program.
- (c) can hold several different values at the same time.
- (d) cannot be reused once it is assigned a value.

- 6. A pointer variable
- (a) contains the data stored at a location in memory.
- (b) contains the address of a memory location.
- (c) can be used in input statements, but cannot be used in output statements.
- (d) can be changed to different values in both input and output statements.

- 7. How would you assign the value of a variable referenced by the pointer a to a variable name?
- (a) a = &name;
- (b) name = &a;
- (c) a = *name;
- (d) name = *a;

- 8. Assume that a and b are pointers to integers and that a points to the variable name. Choose the sentence that best describes the effect of this statement: b = a;
- (a) The value of name is copied into b.
- (b) The memory address stored in a is copied into b.
- (c) The memory address stored in b is copied into a.
- (d) The pointer a is now pointing to a different variable.

### Memory Snapshot Problem

- 9. Assuming that the address of name is 10 and the address of x is 14 (that is, name is stored in memory location 10, and x is stored in memory location 14), give the corresponding snapshots of memory after the following set of statements is executed:
- float name, x=20.5;
- float *a = &x;
- ...
- name = *a;

### Program Analysis

Problems 10-13 refer to the following statements:

```
int i1, i2;
int *p1, *p2;
...
i1 = 5;
p1 = &i1;
i2 = *p1/2 + 10;
p2 = p1;
```

- 10. What is the value of i1?
- 11. What is the value of i2?
- 12. What is the value of p1?
- 13. What is the value of p2?

## PROGRAMMING PROBLEMS

### General Functions

Pointers are often used as function arguments when we want to return more than one value from the function. In each of the following problems, write the indicated function, and then develop a main function for testing the function.

- 14. Write a function that converts radius, diameter, and area measurements for a circle from units of inches and square inches to units of feet and square feet. Assume that the corresponding function prototype statement is

```
void convert_ft(double *r,double *d,double *a);
```

where r, d, and a are pointers to the radius, diameter, and area variables.

- 15. Write a function that reorders the values in three integer variables such that the values are in ascending order. Assume that the corresponding function prototype statement is

```
void reorder(int *a,int *b,int *c);
```

where a, b, and c are pointers to the three variables.

- 16. Write a function that determines the maximum and minimum values from a one-dimensional integer array. Assume that the corresponding function prototype statement is

```
void ranges(int x[],int npts,int *max_ptr, int *min_ptr);
```

where npts contains the number of values in array x, and max_ptr and min_ptr are pointers to the variables in which to store the maximum and minimum values in the array.

- 17. Write a function that returns the double average value of a one-dimensional integer array, in addition to determining the number of values in the array that are greater than the average. Assume that the corresponding function prototype statement is

```
double average(int x[], int npts, int *gtr);
```

where npts contains the number of values in array x and gtr is a pointer to the variable that stores the number of values in x that are greater than the average.

- 18. Write a function that returns the number of positive values, zero values, and negative values in an integer array. Assume that the corresponding function prototype statement is

```
void signs(int x[], int npts, int *npos, int *nzero, int *nneg);
```

where npts contains the number of values in the array x and npos, nzero, and nneg are pointers to variables to store the numbers of positive values, zero values, and negative values in the array.

### Vector Functions

A vector is a group of numerical values that can be represented by a one-dimensional array. These problems develop functions for manipulating values within a vector. Then a reference to the function is requested, to show how to use the function to manipulate groups of values within the vector, instead of manipulating the complete set of
