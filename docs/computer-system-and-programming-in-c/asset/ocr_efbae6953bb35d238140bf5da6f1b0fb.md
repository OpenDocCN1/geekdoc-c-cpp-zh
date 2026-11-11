```
```c
scanf("%d",&a[i][j]);
}
printf("\n enter elements of the second
Matrix:\n");
for(i=0;i< p;i++)
{
for(j=0;j< q;j++)
scanf("%d",&b[i][j]);
}
printf("The first matrix is:\n");
for(i=0;i< m;i++)
{
for(j=0;j< n;j++)
printf("%d ",a[i][j]); //print the first matrix
printf("\n");
}
printf("The second matrix is:\n");
for(i=0;i< p;i++)
{
for(j=0;j< q;j++)
printf("%d ",b[i][j]);
printf("\n");
}
if(n!=p)
{
printf("Aborting!!!!!!\n multiplication of the above matrices not feasible.");
exit(0);
}
else
{
for(i=0;i< m;i++)
{
for(j=0;j< q;j++)
{
c[i][j] = 0;
for(k=0;k< n;k++)
{
c[i][j] = c[i][j] + a[i][k] * b[k][j];
}
}
}
printf("\n multiplication of the above two matrices are:\n\n");
for(i=0;i< m;i++)
{
for(j=0;j< q;j++)
printf("\t%d ",c[i][j]);
```
```

```
```c
}
printf("\n");
}
getch();
}
```
```

# Problem 4

Write a program to input a matrix and print the transpose of a matrix.

# Solution

A matrix which is formed by turning all the rows of a given matrix into columns and vice versa. The transpose of matrix A is written Aᵀ.

![](bbox=[0.61, 0.367, 0.87, 0.415])

The program in C language is as follows:

```
```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int a[3][3],i,j;
    clrscr();
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        {
            printf("\n enter the element");
            scanf("%d",&a[i][j]);
        }
    }
    printf("\n the transpose of the matrix is");
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        {
            printf("\t%d",a[j][i]);
            printf("\n");
        }
    }
    getch();
}
```
```

# Three-Dimensional Array

C allows arrays with more than two dimension, to the limit depending on the compiler.