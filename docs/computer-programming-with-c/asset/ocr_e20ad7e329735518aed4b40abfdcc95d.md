```
```cpp
int a [100] [100];
char symmetric='y';
printf("Enter the no of rows/columns of a square matrix\n");
scanf("%d",&r);
printf("Enter a Matrix\n");
for(i=0;i<=r-1;i++)
{
    for(j=0;j<=r-1;j++)
    {
        scanf("%d",&a[i][j]);
    }
}
/*Check if the matrix is symmetric*/
for(i=0;i<=r-1;i++)
{
    for(j=0;j<=r-1;j++)
    {
        if(a[i][j]!=a[j][i])
        {
            symmetric='n';
        }
    }
}
if(symmetric!='n')
{
    printf("Matrix is symmetric\n");
}
else
{
    printf("Matrix is not symmetric\n");
}
}
```
```

# output

```
```
Enter the no of rows/columns of a square matrix
3
Enter a Matrix
10 10 50
10 50 10
50 10 10
Matrix is symmetric
```
```