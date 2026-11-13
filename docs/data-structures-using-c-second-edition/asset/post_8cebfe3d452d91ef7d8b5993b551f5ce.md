
    printf("%d ", arr[i][j]);
}
getch();
return 0;
}
```

### Output

```
1
1   1
1   2   1
1   3   3   1
1   4   6   4   1
1   5   10  10  5   1
1   6   15  20  15  6   1
```

### 18. In a small company there are five salesmen. Each salesman is supposed to sell three products. Write a program using a 2D array to print (i) the total sales by each salesman and (ii) total sales of each item.

```
#include <stdio.h>
#include <conio.h>
int main()
{
    int sales[5][3], i, j, total_sales=0;
    //INPUT DATA
    printf("\n ENTER THE DATA\n");
    printf("\n ***************\n");
    for(i=0; i<5; i++)
    {
        printf("\n Enter the sales of 3 items sold by salesman %d: ", i+1);
        for(j=0; j<3; j++)
            scanf("%d", &sales[i][j]);
    }
    // PRINT TOTAL SALES BY EACH SALESMAN
    for(i=0; i<5; i++)
    {
        total_sales = 0;
        for(j=0; j<3; j++)
            total_sales += sales[i][j];
        printf("\n Total Sales By Salesman %d = %d", i+1, total_sales);
    }
    // TOTAL SALES OF EACH ITEM
    for(i=0; i<3; i++)
    {
        total_sales=0;
        for(j=0; j<5; j++)
            total_sales += sales[j][i];
        printf("\n Total sales of item %d = %d", i+1, total_sales);
    }
    getch();
    return 0;
}
```

### Output

```
ENTER THE DATA
***************
Enter the sales of 3 items sold by salesman 1: 23 23 45
Enter the sales of 3 items sold by salesman 2: 34 45 63
Enter the sales of 3 items sold by salesman 3: 36 33 43
Enter the sales of 3 items sold by salesman 4: 33 52 35
Enter the sales of 3 items sold by salesman 5: 32 45 64
Total Sales By Salesman 1 = 91
Total Sales By Salesman 2 = 142
Total Sales By Salesman 3 = 112
Total Sales By Salesman 4 = 120
Total Sales By Salesman 5 = 141
Total sales by Salesman = 141
Total sales of item 1 = 158
Total sales of Item 2 = 198
Total sales of item 3 = 250
```

### 19. Write a program to read a 2D array marks which stores the marks of five students in three subjects. Write a program to display the highest marks in each subject.

```
#include <stdio.h>
#include <conio.h>
int main()
{
    int marks[5][3], i, j, max_marks;
    for(i=0; i<=5; i++)
    {
        printf("\nEnter the marks obtained by student %d",i+1);
        for(j=0; j<=3; j++)
        {
            printf("\n marks[%d][%d] = ", i, j);
            scanf("%d", &marks[i][j]);
        }
    }
    for(j=0; j<3; j++)
    {
        max_marks = -999;
        for(i=0; i<=5; i++)
        {
            if(marks[i][j]>max_marks)
            max_marks = marks[i][j];
        }
        printf("\n The highest marks obtained in the subject %d = %d", j+1, max_marks);
    }
    getch();
    return 0;
}
```

### Output

```
Enter the marks obtained by student 1
marks[0][0] = 89
marks[0][1] = 76
marks[0][2] = 100
Enter the marks obtained by student 2
marks[1][0] = 99
marks[1][1] = 90
marks[1][2] = 89
Enter the marks obtained by student 3
marks[2][0] = 67
marks[2][1] = 67
marks[2][2] = 56
Enter the marks obtained by student 4
marks[3][0] = 88
marks[3][1] = 77
marks[3][2] = 66
Enter the marks obtained by student 5
marks[4][0] = 67
marks[4][1] = 78
marks[4][2] = 89
The highest marks obtained in the subject 1 = 99
The highest marks obtained in the subject 2 = 90
The highest marks obtained in the subject 3 = 100
```

## 3.10 OPERATIONS ON TWO-DIMENSIONAL ARRAYS

Two-dimensional arrays can be used to implement the mathematical concept of matrices. In mathematics, a matrix is a grid of numbers, arranged in rows and columns. Thus, using two-dimensional arrays, we can perform the following operations on an m x n matrix:

- **Transpose** Transpose of an m x n matrix A is given as a n x m matrix B, where B_ji = A_ij.
- **Sum** Two matrices that are compatible with each other can be added together, storing the result in the third matrix. Two matrices are said to be compatible when they have the same number of rows and columns. The elements of two matrices can be added by writing: C_{i,j} = A_{i,j} + B_{i,j}
- **Difference** Two matrices that are compatible with each other can be subtracted, storing the result in the third matrix. Two matrices are said to be compatible when they have the same number of rows and columns. The elements of two matrices can be subtracted by writing: C_{i,j} = A_{i,j} - B_{i,j}
- **Product** Two matrices can be multiplied with each other if the number of columns in the first matrix is equal to the number of rows in the second matrix. Therefore, m x n matrix A can be multiplied with a p x q matrix B if n=p. The dimension of the product matrix is m x q. The elements of two matrices can be multiplied by writing: C_{i,j} = \Sigma A_{i,k} B_{k,j} for k=1 to n

## PROGRAMMING EXAMPLES

### 20. Write a program to read and display a 3x3 matrix.

```
#include <stdio.h>
#include <conio.h>
int main()
{
    int i, j, mat[3][3];
    clrscr();
    printf("\n Enter the elements of the matrix ");
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        {
            scanf("%d",&mat[i][j]);
        }
    }
    printf("\n The elements of the matrix are ");
    for(i=0;i<3;i++)
    {
        printf("\n");
        for(j=0;j<3;j++)
        printf("\t %d",mat[i][j]);
    }
    return 0;
}
```

### Output

```
Enter the elements of the matrix
1 2 3 4 5 6 7 8 9
The elements of the matrix are
1 2 3
4 5 6
7 8 9
```

### 21. Write a program to transpose a 3×3 matrix.

```
#include <stdio.h>
#include <conio.h>
void main()
{
    int i, j, mat[3][3], transposed_mat[3][3];
    clrscr();
    printf("\n Enter the elements of the matrix ");
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        scanf("%d", &mat[i][j]);
    }
    printf("\n The elements of the matrix are ");
    for(i=0;i<3;i++)
    {
        printf("\n");
        for(j=0;j<3;j++)
        printf("\t %d", mat[i][j]);
    }
    for(i=0;i<3;i++)
    {
        for(j=0;j<3;j++)
        transposed_mat[i][j] = mat[j][i];
    }
    printf("\n The elements of the transposed matrix are ");
    for(i=0;i<3;i++)
    {
        printf("\n");
        for(j=0;j<3;j++)
        printf("\t %d",transposed_mat[i][j]);
    }
    return 0;
}
```

### Output

```
Enter the elements of the matrix
1 2 3 4 5 6 7 8 9
The elements of the matrix are
1 2 3
4 5 6
7 8 9
The elements of the transposed matrix are
1 4 7
2 5 8
3 6 9
```

### 22. Write a program to input two m x n matrices and then calculate the sum of their corresponding elements and store it in a third m x n matrix.

```
#include <stdio.h>
#include <conio.h>
int main()
{
 int i, j;
 int rows1, cols1, rows2, cols2, rows_sum, cols_sum;
 int mat1[5][5], mat2[5][5], sum[5][5];
 clrscr();
 printf("\n Enter the number of rows in the first matrix : ");
 scanf("%d",&rows1);
 printf("\n Enter the number of columns in the first matrix : ");
 scanf("%d",&cols1);
 printf("\n Enter the number of rows in the second matrix : ");
 scanf("%d",&rows2);
 printf("\n Enter the number of columns in the second matrix : ");
 scanf("%d",&cols2);
 if(rows1 != rows2 || cols1 != cols2)
 {
 printf("\n Number of rows and columns of both matrices must be equal");
 getch();
 exit();
 }
 rows_sum = rows1;
 cols_sum = cols1;
 printf("\n Enter the elements of the first matrix ");
 for(i=0;i<rows1;i++)
 {
 for(j=0;j<cols1;j++)
 scanf("%d",&mat1[i][j]);
 }
 printf("\n Enter the elements of the second matrix ");
 for(i=0;i<rows2;i++)
 {
 for(j=0;j<cols2;j++)
 scanf("%d",&mat2[i][j]);
 }
 for(i=0;i<rows_sum;i++)
 {
 for(j=0;j<cols_sum;j++)
 sum[i][j] = mat1[i][j] + mat2[i][j];
 }
 printf("\n The elements of the resultant matrix are ");
 for(i=0;i<rows_sum;i++)
 {
 printf("\n");
 for(j=0;j<cols_sum;j++)
 printf("\t %d", sum[i][j]);
 }
 return 0;
}
```

### Output

```
Enter the number of rows in the first matrix: 2
Enter the number of columns in the first matrix: 2
Enter the number of rows in the second matrix: 2
Enter the number of columns in the second matrix: 2
Enter the elements of the first matrix
1 2 3 4
Enter the elements of the second matrix
5 6 7 8
The elements of the resultant matrix are
6 8
10 12
```

### 23. Write a program to multiply two m x n matrices.

```
#include <stdio.h>
#include <conio.h>
int main()
{
 int i, j, k;
 int rows1, cols1, rows2, cols2, res_rows, res_cols;
 int mat1[5][5], mat2[5][5], res[5][5];
 clrscr();
 printf("\n Enter the number of rows in the first matrix : ");
 scanf("%d",&rows1);
 printf("\n Enter the number of columns in the first matrix : ");
 scanf("%d",&cols1);
 printf("\n Enter the number of rows in the second matrix : ");
 scanf("%d",&rows2);
 printf("\n Enter the number of columns in the second matrix : ");
 scanf("%d",&cols2);
 if(cols1 != rows2)
 {
 printf("\n The number of columns in the first matrix must be equal
 to the number of rows in the second matrix");
 getch();
 exit();
 }
 res_rows = rows1;
 res_cols = cols2;
 printf("\n Enter the elements of the first matrix ");
 for(i=0;i<rows1;i++)
 {
 for(j=0;j<cols1;j++)
 {
 scanf("%d",&mat1[i][j]);
 }
 }
 printf("\n Enter the elements of the second matrix ");
 for(i=0;i<rows2;i++)
 {
 for(j=0;j<cols2;j++)
 {
 scanf("%d",&mat2[i][j]);
 }
 }
 for(i=0;i<res_rows;i++)
 {
 for(j=0;j<res_cols;j++)
```
