```
for(j = 0 ; j < q ; j++)
{
    c[i][j] = 0;
    for(k = 0 ; k < p ; k++)
        c[i][j] = c[i][j] + a[i][k] * b[k][j];
}
}
else
    printf("Matrix multiplication is invalid");
    printf("Result of matrix multiplication is \\n");
    for(i = 0 ; i < m ; i++)
    {
        for(j = 0 ; j < q ; j++)
            printf("%d \\t", c[i][j]);
        printf("\\n");
    }
}
```

```
The program displays the following output
RUN1 Enter the order of matrix 1 : 3 3
Enter the order of matrix 2 : 3 3
Enter the elements of matrix 1
1 3 5 7 9 11 21 23 25
Enter the elements of matrix 2
25 23 21 11 9 7 5 3 1
Result of matrix multiplication is
83 65 47
329 275 221
903 765 627
RUN2 Enter the order of matrix 1 : 1 2
Enter the order of matrix 2 : 3 4
Matrix multiplication is invalid
```

# Program M5:

Write a program to evaluate the determinant of a matrix.

```
/* determinant.c */
#include<stdio.h>
void main()
{
float a[10][10], det, ratio;
int i, j, k, n;
printf("Enter the order of matrix : ");
scanf("%d", &n);
printf("Enter the elements of matrix \\n");
for(i = 1 ; i <= n ; i++)
for(j = 1 ; j <= n ; j++)
```