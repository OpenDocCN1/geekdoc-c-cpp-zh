
## 9.6.1 Memory Layout

The subscripts in the definition of a two-dimensional array represent rows and columns. This format maps the way that data elements are laid out in the memory. The elements of all arrays are stored contiguously in increasing memory locations, essentially in a single list. If we consider the memory as a row of bytes, with the lowest address on the left and the highest address on the right, a simple array will be stored in memory with the first element at the left end and the last element at the right end. Similarly, a two-dimensional array is stored “row-wise,” starting from the first row and ending with the last row, treating each row like a simple array. This is illustrated below.

![](img/11b034a94fc590add0a7808250a38792_323_0.png)

For a multi-dimensional array, the order of storage is that the first element stored has 0 in all its subscripts, the second has all of its subscripts 0 except for the rightmost, which has a value of 1, and so on. The elements of a 2 × 3 × 3 array will be stored as under.

![](img/11b034a94fc590add0a7808250a38792_323_1.png)

The far right subscript increments first and the other subscripts increment in order from right to left. The sequence numbers 1, 2, ……, 18 represent the location of that element in the list.

### WORKED-OUT PROBLEM 9.7

The program in Fig. 9.8 shows how to find the transpose of a matrix.

**Algorithm**

```text
    Step 1 – Start
    Step 2 – Read a 3 × 3 matrix (a[3][3])
    Step 3 – Initialize the looping counter i = 0
    Step 4 – Repeat Steps 5–9 while i<3
```

```c
printf("\nThe entered matrix is: \n");
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

**Output**

```text
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
The transpose of the matrix is:

1   4   7
2   5   8
3   6   9
```

**Fig. 9.8** *Program to find transpose of a matrix*

### WORKED-OUT PROBLEM 9.8

The program in Fig. 9.9 shows how to multiply the elements of two N × N matrices.

**Program**

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int a1[10][10],a2[10][10],c[10][10],i,j,k,a,b;
clrscr();
printf("Enter the size of the square matrix\n");
scanf("%d",&a);
b=a;
printf("You have to enter the matrix elements in row-wise fashion\n");
for(i=0;i<a;i++)
{
for(j=0;j<b;j++)
{
printf("\nEnter the next element in the 1st matrix=");
scanf("%d",&a1[i][j]);
}
}
for(i=0;i<a;i++)
{
for(j=0;j<b;j++)
{
printf("\n\nEnter the next element in the 2nd matrix=");
scanf("%d",&a2[i][j]);
}
}
printf("\n\nEntered matrices are\n");
for(i=0;i<a;i++)
{
printf("\n");
for(j=0;j<b;j++)
printf(" %d ",a1[i][j]);
}
printf("\n");
for(i=0;i<a;i++)
{
printf("\n");
for(j=0;j<b;j++)
printf(" %d ",a2[i][j]);
}
printf("\n\nProduct of the two matrices is\n");
for(i=0;i<a;i++)
  for(j=0;j<b;j++)
  {
    c[i][j]=0;
    for(k=0;k<a;k++)
    c[i][j]=c[i][j]+a1[i][k]*a2[k][j];
  }
for(i=0;i<a;i++)
{
printf("\n");
for(j=0;j<b;j++)
printf(" %d ",c[i][j]);
}
getch();
}
```

**Output**

```text
Enter the size of the square matrix
2
You have to enter the matrix elements in row-wise fashion
Enter the next element in the 1st matrix=1
Enter the next element in the 1st matrix=0
Enter the next element in the 1st matrix=2
Enter the next element in the 1st matrix=3
Enter the next element in the 2nd matrix=4
Enter the next element in the 2nd matrix=5
Enter the next element in the 2nd matrix=0
Enter the next element in the 2nd matrix=2
Entered matrices are
  1  0
  2  3
  4  5
  0  2
Product of the two matrices is
  4  5
  8 16
```

**Fig. 9.9** *Program for N × N matrix multiplication*

## 9.7 MULTI-DIMENSIONAL ARRAYS

LO 9.5

C allows arrays of three or more dimensions. The exact limit is determined by the compiler. The general form of a multi-dimensional array is

```text
type array_name[s1][s2][s3]...[sm];
```

where s_i is the size of the ith dimension. Some examples are:

```text
int survey[3][5][12];
float table[5][4][5][3];
```

**survey** is a three-dimensional array declared to contain 180 integer type elements. Similarly **table** is a four-dimensional array containing 300 elements of floating-point type.

The array **survey** may represent a survey data of rainfall during the last three years from January to December in five cities.

If the first index denotes year, the second city and the third month, then the element **survey[2][3][10]** denotes the rainfall in the month of October during the second year in city-3.

Remember that a three-dimensional array can be represented as a series of two-dimensional arrays as shown below:

**Year 1**

| Month/City | 1 | 2 | ............. | 12 |
|---|---|---|---|---|
| 1 |  |  |  |  |
| . |  |  |  |  |
| . |  |  |  |  |
| . |  |  |  |  |
| . |  |  |  |  |
| 5 |  |  |  |  |

**Year 2**

| Month/City | 1 | 2 | ............. | 12 |
|---|---|---|---|---|
| 1 |  |  |  |  |
| . |  |  |  |  |
| . |  |  |  |  |
| . |  |  |  |  |
| . |  |  |  |  |
| 5 |  |  |  |  |

ANSI C does not specify any limit for array dimension. However, most compilers permit seven to ten dimensions. Some allow even more.

- Supplying more initializers in the initializer list is a compile time error. (LO 9.2)
- When using expressions for subscripts, make sure that their results do not go outside the permissible range of 0 to size - 1. Referring to an element outside the array bounds is an error. (LO 9.2)
- When using control structures for looping through an array, use proper relational expressions to eliminate “off-by-one” errors. For example, for an array of size 5, the following `for` statements are wrong: (LO 9.2)
  - `for (i = 1; i <= 5; i++)`
  - `for (i = 0; i <= 5; i++)`
  - `for (i = 0; i = 5; i++)`
  - `for (i = 0; i < 4; i++)`
- Referring to a two-dimensional array element like `x[i, j]` instead of `x[i][j]` is a compile time error. (LO 9.3)
- Leaving out the subscript reference operator `[]` in an assignment operation is a compile time error. (LO 9.3)
- When initializing character arrays, provide enough space for the terminating null character. (LO 9.4)
- Make sure that the subscript variables have been properly initialized before they are used. (LO 9.4)
- During initialization of multi-dimensional arrays, it is an error to omit the array size for any dimension other than the first. (LO 9.5)
- While using static arrays, choose the array size in such a way that the memory space is efficiently utilized and there is no overflow condition. (LO 9.6)

## KEY TERMS TO REMEMBER

- **Array:** Is a fixed-size sequenced collection of elements of the same data type. (LO 9.1)
- **One-dimensional array:** Is a list of items that has one variable name and one subscript to access the items. (LO 9.1)
- **Structured data types:** Represent data values that have a structure of some sort. For example, arrays, structures, etc. (LO 9.1)
- **Searching:** Is the process of finding the location of the specified element in the list. (LO 9.2)
- **Sorting:** Is the process of rearranging elements in the list as per ascending or descending order. (LO 9.2)
- **Two-dimensional array:** Is an array of arrays that has two subscripts for accessing its values. It is used to represent table or matrix data. (LO 9.3)
- **Multi-dimensional array:** Is an array with more than one dimension. Examples of multi-dimensional arrays are two-dimensional array, three-dimensional array and so on. (LO 9.5)
- **Dynamic arrays:** Are the arrays declared using dynamic memory allocation technique. (LO 9.6)
- **Dynamic memory allocation:** Is the process of allocating memory at run time. (LO 9.6)
- **Static arrays:** Are the arrays declared using static memory allocation technique. (LO 9.6)
- **Static memory allocation:** Is the process of allocating memory at compile time. (LO 9.6)

## BRIEF CASES

### 1. Median of a List of Numbers

When all the items in a list are arranged in an order, the middle value which divides the items into two parts with equal number of items on either side is called the *median*. Odd number of items have just one
