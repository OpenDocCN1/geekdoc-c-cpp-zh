```
```cpp
}
printf("Enter Matrix b\\n");
for(i=0;i<=r2-1;i++)
{
    for(j=0;j<=c2-1;j++)
    {
        scanf("%d",&b[i][j]);
    }
}
/*perform multiplication*/
printf("Multiplication is\\n");
for(i=0;i<=r1-1;i++)
{
    for(j=0;j<=c2-1;j++)
    {
        Res[i][j]=0;
        for(k=0;k<=c1-1;k++)
        {
            Res[i][j]+=a[i][k]*b[k][j];
        }
        printf("%d ",Res[i][j]);
    }
    printf("\\n");
}
}
else
{
    printf("Multiplication is not possible\\n");
}
/*end of main*/
```
```

# Output:

```
```text
Enter the order of the matrix a 2 2
Enter the order of the matrix b 2 2
Enter Matrix a
10 2
1 0
Enter Matrix b
5 6
10 5
Multiplication is
70 70
5 6
```
```