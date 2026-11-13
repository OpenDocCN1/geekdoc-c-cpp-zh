A pointer to a three-dimensional array can be declared as,

```
int arr[2][2][2]={1,2,3,4,5,6,7,8};
int (*parr)[2][2];
parr = arr;
```

We can access an element of a three-dimensional array by writing,

```
arr[i][j][k] = *(*(*(arr+i)+j)+k)
```

# PROGRAMMING EXAMPLE

# 27. Write a program which illustrates the use of a pointer to a three-dimensional array.

```
#include <stdio.h>
#include <conio.h>
int main()
{
    int i,j,k;
    int arr[2][2][2];
    int (*parr)[2][2] = arr;
    clrscr();
    printf("\n Enter the elements of a 2 x 2 x 2 array: ");
    for(i = 0; i < 2; i++)
    {
        for(j = 0; j < 2; j++)
        {
            for(k = 0; k < 2; k++)
                scanf("%d", &arr[i][j][k]);
        }
    }
    printf("\n The elements of the 2 x 2 x 2 array are: ");
    for(i = 0; i < 2; i++)
    {
        for(j = 0; j < 2; j++)
        {
            for(k = 0; k < 2; k++)
                printf("%d", *(*(*(parr+i)+j)+k));
        }
    }
    getch();
    return 0;
}
```

# Output

Enter the elements of a 2 x 2 x 2 array: 1 2 3 4 5 6 7 8
The elements of the 2 x 2 x 2 array are: 1 2 3 4 5 6 7 8

# Note

In the printf statement, you could also have used * (*(*(arr+i)+j)+k) instead of *(*(*(parr+i)+j)+k).

# 3.15 SPARSE MATRICES

Sparse matrix is a matrix that has large number of elements with a zero value. In order to efficiently utilize the memory, specialized algorithms and data structures that take advantage of the sparse structure should be used. If we apply the operations using standard matrix structures and algorithms to sparse matrices, then the execution will slow down and the matrix will consume large amount of memory. Sparse data can be easily compressed, which in turn can significantly reduce memory usage.