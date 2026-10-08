
# 492 Multidimensional Arrays

d. Two matrices of any size may be multiplied.

2. Write code to prove or disprove the statements of Question 1.

3. Given the following two-dimensional arrays x and y, show the result of each of the following operations.

| array x | array y |
| :--- | :--- |
| 2.5 4.2 5.2 6.4 | 3.6 5.8 1.5 6.3 |
| 4.2 2.6 1.2 9.8 | 4.3 2.4 4.5 5.7 |
| 3.5 8.5 5.9 5.3 | 5.3 6.7 3.4 2.9 |
| 1.3 2.1 3.2 4.8 | 3.6 9.1 7.8 6.9 |

```
a. for(i = 0; i < 4; i++)
x[2][1] = y[1][1];
b. for(i = 0; i < 4; i++)
x[i][3] = y[i][1] + y[i][2];
c. for(i = 0; i < 4; i++)
x[1][3] = y[i][1] + y[3][i];
d. for(i = 0; i < 4; i++)
for(j = 0; j < 4; j++)
x[i][j] = 2 * y[i][j] + 5.5;
```

+ 4. Given the two-dimensional integer array x[4][5], write the code to perform the following operations.
   a. To compute the sum of each row and store the sum in the corresponding element of a one-dimensional array.
   b. To compute the sum of each column and store the sum in the corresponding element of a one-dimensional array.
   c. To compute the sum of all the elements of the array.
   d. To output the rows, columns, row sums by the side of rows, column sums under the columns, and the total sum of all elements under the rows in the same line as the column sums.
5. Given the square matrix x[5][5], write the code segments to perform the following operations.
   a. To compute the sum of the main diagonal.
   b. To compute the sum of the minor diagonal.
   c. To compute the sum of the elements in the upper triangular matrix.
   d. To compute the sum of the elements in the lower triangular matrix.

# 8.5 Passing Arrays to Functions

A two-dimensional array is passed to a function as an argument by array name. The value of the name of the array is actually an address so the location of the array is passed to the function. In the function prototype the data type of the array and the square brackets for the first dimension without the row size and the second square bracket with the number of columns specified must be provided. The array name in the function prototype is optional.

# 8.5.1 Passing Fixed Size Arrays

The fixed size arrays are passed to the functions by array name. The following examples show the function prototype with the array parameters for fixed size arrays.

```
#define IMAX 3
#define JMAX 4

void func(int [][JMAX]); /* one form of function prototype */
```

It is necessary to have the number of columns in the function prototype and the function header, because the way the computer locates the address of any element in the array requires the number of columns. The number of elements in each row is the number of columns. The address of any element of the array is equal to the number of full rows preceding the row in which the element is located multiplied by the number of columns plus the position in the row of the element under consideration.

Address of any element = number of full rows * JMAX + column index of the element under consideration. Where JMAX is the number of columns.
arr[i][j] is in position i * JMAX + j

> Programming Warning: To compute the address, the number of columns is required. The number of columns must be specified in both the prototype and the function header parameters.

For example, the element x[1][2] is located after one full row and two elements. In an array declared as x[3][4], the element x[1][2] is located after 1 * 4 + 2 other elements.

# 494 Multidimensional Arrays

The following program shows the passing of two-dimensional arrays as arguments and parameters to functions that input, add, and output them.

```
#include <stdio.h>
#define IMAX 3
#define JMAX 4

void funcinput(int [][JMAX]);
void funcadd(int [][JMAX], int [][JMAX], int [][JMAX]);
void funcoutput(int [][JMAX]);

int main ()
{
    int a[IMAX][JMAX], b[IMAX][JMAX], c[IMAX][JMAX];
    funcinput(a);
    funcoutput(b);
    funcadd(a, b, c);
    printf("Array a:\n\n");
    funcoutput(a);
    printf("Array b:\n\n");
    funcoutput(b);
    printf("Array c:\n\n");
    funcoutput(c);
    return 0;
}

void funcinput (int arr[][JMAX])
{
    int i, j;
    for(i=0; i < IMAX; i++){
        for(j=0; j < JMAX; j++){
            scanf("%d", &arr[i][j]); /* assume IMAX*JMAX values are found for each array */
        }
    }
    return;
}
```

```
void funcadd(int a[][JMAX])
```

Notice that the storage for the arrays a, b, and c is allocated in the main function where they are declared. Storage must be in the main function if it is to be available to all the subfunctions. Arrays a and b are passed one at a time to the function input() by array name in separate calls to the function. The input values found by the function input() are stored in array a and array b. The arrays a, b, and c are passed to the funcadd to add a and b element-element and store the sums in elements of array c. All three arrays are passed by name. The arrays a, b, and c are passed one at a time to the funcoutput() to print them.

# 8.5.2 Passing Array Elements

Two-dimensional arrays may be passed to functions element-element. Passing elements of two-dimensional array to a function may be either by value or address. The following examples show the passing of two-dimensional array elements.

# 496 Multidimensional Arrays

```
#include <stdio.h>
#define IMAX 3
#define JMAX 4

void funcadd(int, int, int *);

int main()
{
    int a[IMAX][JMAX], b[IMAX][JMAX], c[IMAX][JMAX];
    int i, j, x, y;
    ..
    for(i = 0; i < IMAX; i++)
    {
        for(j = 0; j < JMAX; j++)
        {
            funcadd(a[i][j], b[i][j], &c[i][j]);
        }
    }
    ..
}

void funcadd(int a1, int b1, int *c1)
{
    *c1 = a1 + b1;
    return;
}
```

The arrays a and b cannot be passed by value. But by passing by value, the arrays are protected against inadvertent change in the function. The elements of array c are passed by address as array c to receive the result of the addition.

# 8.5.3 Review Questions

+ 1. Indicate whether the following statements are true or false.
    a. In C, two-dimensional arrays may be passed to a function by name.
    b. Passing a two-dimensional array by name means passing the two-dimensional array by value.
    c. In the prototype of the function with array parameters, the second dimension of any two-dimensional array must be specified.
    d. A two-dimensional array passed to a function may be manipulated by rows and columns in the function.
    e. Two-dimensional arrays may be passed to a function element-element either by value or address if they are to be manipulated in the function.

+ 2. Write code to prove or disprove statements of Question 1.

+ 3. Write a function to receive an array of pressure values and identify the maximum value of the pressure in each row and output the array and the maximum value of each row at the end of each row.

+ 4. Write a main function and the following other functions:
a. Write a function to input the temperature measurements in cooling towers arranged in 10 rows and 5 columns.
b. Write a function to determine the average temperature in each of the 10 rows and in each of the 5 columns.
c. Write a function to output the rows and columns and the average temperatures in each row and column. The row averages must be printed at the end of each row and the column averages must be printed at the end of each column.

# 8.6 Higher-Dimensional Arrays

In science and engineering, mathematical modeling of physical problems for simulation and design is very common. Often problems involve three dimensions and sometimes even four. Problems having three-dimensional geometry require three-dimensional arrays. Three-dimensional problems such as airflow over an airfoil, wave propagation in solid and liquid media, vibration of three-dimensional objects, and stress analysis in three-dimensional structures dealing with three space variables and, in some cases, a time variable requires four dimensions.

# 8.6.1 Declaration and Storage Allocation

In C a three-dimensional array may be declared as planes, rows, and columns. The general form of the declaration is:

```
data type array-name[number of planes][number of rows][number of columns];
```
