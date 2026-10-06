
## 2. Initialization of Array

The initialization of an array is to assign values to the array elements when declaring an array. To array of basic types, initialization assigns values to array elements; to object array, every element is a class object, so the initialization needs to call the constructor of the object. We will introduce object arrays later in detail.

When declaring an array, we can initialize the array elements. For example,

```
int a[3]={1,1,1};
```

indicates that we declare an array of int type has three elements, and values of a[0], a[1], a[2] are all 1. If we list all the initial values of array elements during the array declaration, then we need not explicitly give the number of elements. The statement below is completely equivalent to the statement above.

```
int a[]={1,1,1};
```

We can only initialize part of the array elements during an array declaration. For example, when declaring a float type array, we can assign the first three elements 1.0, 2.0, and 3.0 respectively, and it can be written as

```
float fa[5]={1.0, 2.0, 3.0};
```

Here, the number of array elements must be specified, and it is unnecessary to give any explanation for the last two elements. Note that we can only initialize all the elements or the first elements of an array, and we cannot initialize array elements selectively.

The initialization of a multidimensional array follows the same rule as a one-dimensional array. Moreover, if we give initial values to all the elements, the subscript of the first dimension doesn't need to be declared explicitly. For example,

```
int a[2][]={1, 0, 0, 0, 1, 0};
```

equals to

```
int a[][3]={1, 0, 0, 0, 1, 0};
```

Elements of a multidimensional array can be grouped according to the subscript of the first dimension, and we can use braces to enclose each group. For a two-dimensional array, we can use braces to enclose the members of the same row into a group. The statement below is completely equivalent to the statement above

```
int a[2][3]={{1, 0, 0}, {0, 0, 1, 0}};
```

The writing form of grouping by braces is easy to recognize and understand.

## 6.1 Arrays 203

### 6.1.3 Using Arrays as Function Parameters

Array elements and array names can be used as parameters of functions to achieve data passing and data sharing between functions.

We can use an array element as an actual parameter when calling a function, which is completely equivalent to using a variable (or object) of the same type as an actual parameter.

If we use an array name as a parameter of a function, the actual parameter and the formal parameter should be both the array name and be of the same type. Different from common variables, **when we use an array name to pass data, we are actually passing the starting address of the array.** The starting address of the formal parameter is array, and the following elements of the formal and the actual parameter arrays correspondingly share the same addresses. Thus, the sum of elements of the actual parameter array should not be less than that of the formal parameter array. It is noticeable if we change the values of the formal parameter array elements in the called function, the values of the actual parameter array elements in the calling function will also be changed.

Example 6.2: Using array name as function parameter.
The program below first initializes a matrix and outputs each element of the matrix in the main function; then, a function is called to sum the elements in each row and save the result as the first element of each row. At last, the main function outputs the sum of elements in each row.

```
//2.cpp
#include <iostream>
using namespace std;
void RowSum(int A[][4], int row)
    //Compute the sum of elements in each row of the two dimensional
    //Array A; row is the number of rows
{
    for (int i = 0; i < row; i++)
    {
        for(int j = 1; j < 4; j++)
            A[i][0] += A[i][j];
    }
}
int main()            //main function
{
    int Table[3][4] = {{1,2,3,4},{2,3,4,5},{3,4,5,6}};
    //declare and initialize an array
    for (int i = 0; i < 3; i++) //Output array elements
```

## 6 Arrays, Pointers, and Strings

```
{
for (int j = 0; j < 4; j++)
    cout << Table[i][j] << " ";
cout << endl;
}
```

RowSum(Table,3); //Call the subfunction to compute the //sum of elements of each row
for (i = 0; i < 3; i++) //Output the results

```
{
cout << "Sum of row " << i << " is " <<Table[i][0] << endl;
}
```

The result of the program is:

1 2 3 4
2 3 4 5
3 4 5 6
Sum of row 0 is 10
Sum of row 1 is 14
Sum of row 2 is 18

Analyzing the output result of the program carefully, we can find that before calling the function, Table[i] is 1, 2, 3, 4; 2, 3, 4, 5; 3, 4, 5, 6. Sum of row 0 is 10, Sum of row 1 is 14, Sum of row 2 is 18.

## 6.1.4 Object Arrays

Like basic types, we can only initialize all the elements or the first elements of an array, and we cannot initialize array elements selectively.

The initialization of a multidimensional array follows the same rule as a one-dimensional array. Moreover, if we give initial values to all the elements, the subscript of the first dimension doesn't need to be declared explicitly.

