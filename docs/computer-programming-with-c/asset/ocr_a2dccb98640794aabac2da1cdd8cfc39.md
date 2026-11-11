```
```c++
{
    scanf("%d",&a[i][j]);
    }
}
printf("Enter the element to be searched:\n");
scanf("%d",&x);
for(i=0;i<=r-1;i++)
{
    for(j=0;j<=c-1;j++)
    {
        if(a[i][j]==x)
        {
            posRow=i;
            posCol=j;
        }
    }
}
if(posRow!=-1 && posCol!=-1)
{
    printf("Element present at row %d and column %d \n" ,posRow, posCol);
}
else
{
    printf("Element not found\n");
}
}
```
```

**Output**

Enter the number of rows and columns of the array:
3 4
Enter a 2D array
10 15 20 25
30 35 40 45
50 55 60 65
Enter the element to be searched:
40
Element present at row 1 and column 2

# **Solved Example 6.16**

Write a program to take a square matrix as input from the user and to calculate the sum of diagonal elements of the matrix.