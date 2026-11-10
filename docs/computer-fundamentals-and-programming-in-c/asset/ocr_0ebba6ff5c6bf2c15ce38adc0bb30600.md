and its use is not encouraged, but it does illustrate how the elements are actually stored.

```
for(i = 0; i < 12; i++)
    a[0][i] = i;
```

This trick is possible because C does not do run-time range checking of array subscripts. The following code is also valid for the two-dimensional array a[4][3] of integer type

```
for(i = 0; i < 12; ++i)
    scanf("%d", &a[0][i]);
```

Readers may have noticed that in C the rightmost subscript of a two-dimensional array varies faster than the leftmost (in fact, there are no multidimensional arrays in C, but array of arrays). This fact suggests that the array is stored in a ‘row major addressing’ format. So the array equation for element ‘a[m][n]’ of type T is as follows:

```
Address of (a[i][j]) = address of a[0][0] + (i * n + j)
```

The array equation is important. In C, it is hidden from the programmer; the compiler automatically computes the necessary code whenever an array reference is made. The obvious advantage is that the number of rows is not required in the array equation, the address of an element does not have to be computed. That is why, when a two-dimensional array is passed to a function, it is not always necessary to specify the first dimension of the corresponding formal parameter in the function header of the function definition. But for higher-dimensional arrays, the equation gets more and more complicated.

Brian Kernighan and Dennis Ritchie tried to create a unified treatment of arrays and pointers, one that would expose rather than hide the array equation in the compiler’s code. It has been already discussed that a[i] = *(a + i). Therefore, following the same concept, a two-dimensional array can be expressed as follows:

```
a[i][j] = *(a[i] + j) = *(*(a + i)[j]) = *(*(a + i) + j)
```

The array equation discussed above is a consequence of the aforesaid notations in the case of a two-dimensional array. The following program illustrates the facts just discussed.

# EXAMPLE

```
27. #include <stdio.h>
int main()
{
    int a[2][3]={10,20,30,40,50,60};
    int i,j;
    for(i=0;i<2;++i)
    {
        printf("\\n");
        for(j=0;j<3;++j)
            printf("%d\\t",*(*(a+i)+j));
    }
    return 0;
}
```

# Output

```
10 20 30
40 50 60
```

The same output will result if the statement

```
printf("%d\\t",*(*(a+i)+j));
```

is replaced by the following equivalent statements,

```
printf("%d\\t",*(a[i]+j));
printf("%d\\t",*(*(a+i)[j]));
printf("%d\\t",*(&a[0][0]+i*3+j));
```

Thus, to evaluate either expression, a total of five values must be known.

+   - The address of the first element of the array, which is returned by the expression a, i.e., the name of the array
+   - The size of the type of the elements of the array, in this case `sizeof(int)`
+   - The second dimension of the array
+   - The specific index value for the first dimension, 2 in this case
+   - The specific index value for the second dimension, 3 in this case

# 13.14.1 Passing Two-dimensional Array to a Function

The following are several alternative ways in C to handle an array passed to a function. They differ in the formal parameter. For illustration, the following C statements are considered.

```
#define MAX_ROWS 10
#define MAX_COLS 10
int A[MAX_ROWS][MAX_COLS];
```

When data is accessed in our matrix using the notation

```
A[i][j]
```

the location for this data is computed using

```
&A[0][0] + MAX_COLS * i + j
```

Some interesting information about a two-dimensional array A[10][10] is as follows.

+   - `&A[0][0]` is the base address.
+   - `A[0]` is the base address.
+   - `A` is the base address.
+   - `&A[0]` is the base address.

But these are not interchangeable. For instance,

```
&A[0][0] + 1    points to A[0][1].
A[0] + 1        points to A[0][1].
A + 1           points to A[1][0].
                (A + 1 is the same as &A[1] and points to row 1.)
&A[0] + 1       points to A[1][0].
```