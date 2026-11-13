
int *ptr[10];
int p = 1, q = 2, r = 3, s = 4, t = 5;
ptr[0] = &p;
ptr[1] = &q;
ptr[2] = &r;
ptr[3] = &s;
ptr[4] = &t;

Can you tell what will be the output of the following statement?

```
printf("%d", *ptr[3]);
```

The output will be 4 because ptr[3] stores the address of integer variable s and *ptr[3] will therefore print the value of s that is 4. Now look at another code in which we store the address of three individual arrays in the array of pointers:

```
int main()
{
    int arr1[]={1,2,3,4,5};
    int arr2[]={0,2,4,6,8};
    int arr3[]={1,3,5,7,9};
    int *parr[3] = {arr1, arr2, arr3};
    int i;
    for(i = 0;i<3;++i)
        printf("%d\n", *parr[i]);
    return 0;
}
```

Output
1 0 1

Surprised with this output? Try to understand the concept. In the for loop, parr[0] stores the base address of arr1 (or, &arr1[0]). So writing "*parr[0] will print the value stored at &arr1[0]. Same is the case with *parr[1] and *parr[2].

## 3.9 TWO-DIMENSIONAL ARRAYS

Till now, we have only discussed one-dimensional arrays. One-dimensional arrays are organized linearly in only one direction. But at times, we need to store data in the form of grids or tables. Here, the concept of single-dimensional arrays is extended to incorporate two-dimensional data structures. A two-dimensional array is specified using two subscripts where the first subscript denotes the row and the second denotes the column. The C compiler treats a two-dimensional array as an array of one-dimensional arrays. Figure 3.26 shows a two-dimensional array which can be viewed as an array of arrays.

### 3.9.1 Declaring Two-dimensional Arrays

Any array must be declared before being used. The declaration statement tells the compiler the name of the array, the data type of each element in the array, and the size of each dimension. A two-dimensional array is declared as:

```
data_type array_name[row_size][column_size];
```

![](img/be6359df08208122bec6fad1103de211_106_0.png)

Therefore, a two-dimensional m x n array is an array that contains m x n data elements and each element is accessed using two subscripts, i and j, where i < m and j < n.

For example, if we want to store the marks obtained by three students in five different subjects, we can declare a two-dimensional array as:

```
int marks[3][5];
```

Figure 3.26 Two-dimensional array

In the above statement, a two-dimensional array called marks has been declared that has m(3) rows and n(5) columns. The first element of the array is denoted by marks[0][0], the second element as marks[0][1], and so on. Here, marks[0][0] stores the marks obtained by the first student in the first subject, marks[1][0] stores the marks obtained by the second student in the first subject.

The pictorial form of a two-dimensional array is shown in Fig. 3.27.

| Rows \ Columns | Col 0 | Col 1 | Col 2 | Col 3 | Col 4 |
|---|---|---|---|---|---|
| Row 0 | marks[0][0] | marks[0][1] | marks[0][2] | marks[0][3] | marks[0][4] |
| Row 1 | marks[1][0] | marks[1][1] | marks[1][2] | marks[1][3] | marks[1][4] |
| Row 2 | marks[2][0] | marks[2][1] | marks[2][2] | marks[2][3] | marks[2][4] |

Figure 3.27 Two-dimensional array

Hence, we see that a 2D array is treated as a collection of 1D arrays. Each row of a 2D array corresponds to a 1D array consisting of n elements, where n is the number of columns. To understand this, we can also see the representation of a two-dimensional array as shown in Fig. 3.28.

```
marks[0] - marks[0] marks[1] marks[2] marks[3] marks[4]
marks[1] - marks[0] marks[1] marks[2] marks[3] marks[4]
marks[2] - marks[0] marks[1] marks[2] marks[3] marks[4]
```

Figure 3.28 Representation of two-dimensional array marks[3][5]

Although we have shown a rectangular picture of a two-dimensional array, in the memory, these elements actually will be stored sequentially. There are two ways of storing a two-dimensional array in the memory. The first way is row major order and the second is the column major order. Let us see how the elements of a 2D array are stored in a row major order. Here, the elements of the first row are stored before the elements of the second and third rows. That is, the elements of the array are stored row by row where n elements of the first row will occupy the first n locations. This is illustrated in Fig. 3.29.

![](img/be6359df08208122bec6fad1103de211_107_0.png)

Figure 3.29 Elements of a 3 x 4 array in row major order

However, when we store elements in a column major order, the elements of the first column are stored before the elements of the second and third column. That is, the elements of the array are stored column by column where n elements of the first column will occupy the first n locations. This is illustrated in Fig. 3.30.

![](img/be6359df08208122bec6fad1103de211_107_1.png)

Figure 3.30 Elements of a 4 x 3 2D array in column major order

In one-dimensional arrays, we have seen that the computer does not keep track of the address of every element in the array. It stores only the address of the first element and calculates the address of other elements from the base address (address of the first element). Same is the case with a two-dimensional array. Here also, the computer stores the base address, and the address of the other element is calculated using the following formula.

If the array elements are stored in column major order, Address(A[I][J]) = Base_Address + w{M * (J - 1) + (I - 1)}

And if the array elements are stored in row major order, Address(A[I][J]) = Base_Address + w{N * (I - 1) + (J - 1)}

where w is the number of bytes required to store one element, N is the number of columns, M is the number of rows, and I and J are the subscripts of the array element.

### Example 3.5

Consider a 20 x 5 two-dimensional array marks which has its base address = 1000 and the size of an element = 2. Now compute the address of the element, marks[18][4] assuming that the elements are stored in row major order.

**Solution**

```
Address(marks[I][J]) = Base_Address + w{N * (I - 1) + (J - 1)}
Address(marks[18][4]) = 1000 + 2 {5(18 - 1) + (4 - 1)}
= 1000 + 2 {5(17) + 3}
= 1000 + 2 {88}
= 1000 + 176 = 1176
```

### 3.9.2 Initializing Two-dimensional Arrays

Like in the case of other variables, declaring a two-dimensional array only reserves space for the array in the memory. No values are stored in it. A two-dimensional array is initialized in the same way as a one-dimensional array is initialized. For example,

```
int marks[2][3]={90, 87, 78, 68, 62, 71};
```

Note that the initialization of a two-dimensional array is done row by row. The above statement can also be written as:

```
int marks[2][3]={{90,87,78},{68, 62, 71}};
```

The above two-dimensional array has two rows and three columns. First, the elements in the first row are initialized and then the elements of the second row are initialized. Therefore, marks[0][0] = 90 marks[0][1] = 87 marks[0][2] = 78 marks[1][0] = 68 marks[1][1] = 62 marks[1][2] = 71

In the above example, each row is defined as a one-dimensional array of three elements that are enclosed in braces. Note that the commas are used to separate the elements in the row as well as to separate the elements of two rows.

In case of one-dimensional arrays, we have discussed that if the array is completely initialized, we may omit the size of the array. The same concept can be applied to a two-dimensional array, except that only the size of the first dimension can be omitted. Therefore, the declaration statement given below is valid.

```
int marks[][3] = {{90,87,78},{68, 62, 71}};
```

In order to initialize the entire two-dimensional array to zeros, simply specify the first value as zero. That is,

```
int marks[2][3] = {0};
```

The individual elements of a two-dimensional array can be initialized using the assignment operator as shown here.

```
marks[1][2] = 79;
```

or

```
marks[1][2] = marks[1][1] + 10;
```

### 3.9.3 Accessing the Elements of Two-dimensional Arrays

The elements of a 2D array are stored in contiguous memory locations. In case of one-dimensional arrays, we used a single for loop to vary the index i in every pass, so that all the elements could be scanned. Since the two-dimensional array contains two subscripts, we will use two for loops to scan the elements. The first for loop will scan each row in the 2D array and the second for loop will scan individual columns for every row in the array. Look at the programs which use two for loops to access the elements of a 2D array.

## PROGRAMMING EXAMPLES

### 16. Write a program to print the elements of a 2D array.

```
#include <stdio.h>
#include <conio.h>
int main()
{
    int arr[2][2] = { 12, 34, 56,32};
    int i, j;
    for(i=0;i<2;i++)
    {
        printf("\n");
        for(j=0;j<2;j++)
        printf("%d\t", arr[i][j]);
    }
    return 0;
}
```

**Output**

12      34
56      32

### 17. Write a program to generate Pascal's triangle.

```
#include <stdio.h>
#include <conio.h>
int main()
{
    int arr[7][7]={0};
    int row=2, col, i, j;
    arr[0][0] = arr[1][1] = 1;
    while(row < 7)
    {
        arr[row][0] = 1;
        for(col = 1; col <= row; col++)
        arr[row][col] = arr[row-1][col-1] + arr[row-1][col];
        row++;
    }
    for(i=0; i<7; i++)
    {
        printf("\n");
        for(j=0; j<=i; j++)
```
