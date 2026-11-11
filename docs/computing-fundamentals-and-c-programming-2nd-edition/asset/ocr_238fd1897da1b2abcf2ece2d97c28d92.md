```
    printf("\nThe entered matrix
    is: \n");
    for(i=0;i<3;i++)
    {
        printf("\n");
        for(j=0;j<3;j++)
        {
            printf("%d\t",a[i][j]);
        }
    }
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
            b[i][j]=a[j][i];
    }
    printf("\n\nThe transpose of the matrix is: \n");

    for(i=0;i<3;i++)
    {
        printf("\n");
        for(j=0;j<3;j++)
        {
            printf("%d\t",b[i][j]);
        }
    }
    getch();
    }
```

```
    Output
    Enter a 3 X 3 matrix:
    a[0][0] = 1
    a[0][1] = 2
    a[0][2] = 3
    a[1][0] = 4
    a[1][1] = 5
    a[1][2] = 6
    a[2][0] = 7
    a[2][1] = 8
    a[2][2] = 9
    The entered matrix is:
        1    2    3
        4    5    6
        7    8    9
```