

In the first example, the `for` loop initializes the value of all the elements of the array to zero. In the second example, the `for` loop initializes the value 5 to `mark[0]`, 10 to `mark[1]` and so on. In the third example, the `scanf()` function reads values from the user for the array. Similar to the `for` loop, initialization of an array can be carried out using `while` and `do-while` loops.

### Rules for initializing an array

- If the number of initializers is less than the number of elements in the array, the remaining elements are set to zero. For example, int value[5] = {21, 5, 79};
- It is an error to specify more initializers than the number of elements in the array. For example, int value[2] = {4, 3, 2, 1, 5, 7};
- It is not necessary to specify the length of an array, explicitly in case if initializers are provided for the array during declaration itself. For example, int value[] = { 5, 4 };
- A character array can be initialized by a string constant, resulting in the first element of the array being set to the first character in the string, the second element to the second character and so on. The array also receives the terminating '\0' in the string constant. The initialization may be char name[7] = "GANDHI"; which is equivalent to char name[7] = {'G', 'A', 'N', 'D', 'H', 'I', '\0'};

## 1.13 Two-Dimensional Arrays

Arrays whose elements are specified by two subscripts are referred as two-dimensional arrays or two dimensional arrays. A two-dimensional array is defined in the same manner as a one dimensional array except that it requires two pairs of square brackets for two subscripts. The two-dimensional array is also referred as a matrix. Each subscript must be expressed as a non-negative integer. The general form or the syntax of a two-dimensional array is

```
storageType dataType arrayName[rowsize][colsize];
```

where the storageType may be either auto, or static, or extern. The storageType while declaring an array is optional. The dataType specifies the type of element that will be stored in the array. The arrayName is the name used to identify the array. The rules for naming array names are same as identifiers. The rowsize and colsize are positive value integer constants. These two subscripts indicate, the number of array elements associated with each subscript. Two square braces are used to indicate the values of two subscripts. For example,

```
int mark[2][2];
```

defines a table as an integer array having 2 rows and 2 columns. An array element starts with an index zero and so the individual elements of the array will be

```
mark[0][0] mark[0][1]
mark[1][0] mark[1][1]
```

The first element is stored in the memory location [0] [0], followed by the second element in [0] [1] and so on, and the last element will be stored in the memory location [1] [1]. The total number of elements of a two-dimensional array can be calculated from the product number of rows and the number of columns. An m×n, two-dimensional array can have a table of values having m rows and n columns as shown in Fig. 1.10.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_64_0.png)

Fig. 1.10 : Memory allocation of a double-dimensional array.

The product of rowsize and colsize indicates the maximum number of elements of the array. It is not compulsory that the rowsize and colsize should be equal. Care must be taken to initialize the values of array elements. The colsize subscript increases most rapidly and the rowsize subscript increases least rapidly (i.e., all the elements of the first row will be assigned and then all the second row will be assigned and so on).

### 1.13.1 Initializing Two-Dimensional Arrays

Like one dimensional arrays, a two dimensional array can also be initialized. Arrays can be initialized by the following ways,

- Initializing an array during declaration
- Initializing an array using loops.

### Initializing an array during declaration

Similar to one dimensional arrays, a two dimensional array can also be initialized with one or more values during its declaration. The general form or the syntax of initializing an array during declaration is

```
StorageType dataType arrayName[rowsize] [colsize] = { List of Values };
```

where the storageType, may be either auto, or register, or static, or extern. The storageType while declaring an array is optional. The dataType specifies the type of elements that will be stored in the array. The arrayName is the name used to identify the array. The rules for naming array names are same as identifiers. Note that an array should not have the same name as an ordinary variable in the same block or function. The rowsize and colsize are positive value integer constants, which indicate the number of array elements associated with each subscript.

For example,

```
int mark[4][2] = { {84, 56},
       {92, 67},
       {75, 78},
       {69, 89} };
```

The first subscript ranges from 0 to 3 and the second subscript ranges from 0 to 1. In the first case, the first inner pair of braces are assigned to the array elements in the first row, the values of second inner pair of braces are assigned to the array elements in the second row and so on. An outer pair of braces is required, containing the inner pair. Each line contains 2 marks of one student separated by commas and enclosed in braces and separated from the next student's marks by using the comma operator and the whole array is enclosed in a pair of braces. The array mark can also be declared as

```
int mark[4][2] = {84, 56, 92, 67, 75, 78, 69, 89};
```

The results of the initial assignment are,

```
mark[0][0] = 84       mark[1][0] = 56
mark[0][1] = 92       mark[1][1] = 67
mark[0][2] = 75       mark[1][2] = 78
mark[0][3] = 69       mark[1][3] = 89
```

Consider the following initializations of two-dimensional array.

```
int rank[3][2] = {1, 2, 3, 4, 5, 6};
int rank[][2] = {1, 2, 3, 4, 5, 6};
float amount[2][3] = {25.6, 90.2, 89.4, 72.6};
```

In the first example, the size of the array is 6 (i.e., 3*2) and the values 1, 2, 3, 4, 5, 6 are assigned to the variable rank[0][0],rank[0][1],...,rank[2][1] respectively. In the second example, the rowsize is missing. While initializing an array, the second dimension (i.e., colsize) is necessary, but the first dimension (i.e., rowsize) is optional. If the row size is not assigned, the compiler allocates enough memory space for all the elements given for initialization. The first and second examples are the same. In the third example, the number of values in the array is less than the size of the array and so the values 25.6, 90.2, 89.4, 72.6 will be assigned to the variable amount[0][0], amount[0][1], amount[0][2] and amount[1][0] and the remaining variables amount[1][1] and amount[1][2] will be set to zero automatically.

### Program 1.16

```
/* Program to calculate the sum of all elements in a matrix. */
/* summat.c */
#include<stdio.h>
void main()
{
    int a[10][10], i, j, m, n, sum = 0;
    printf("Enter the order of matrix : ");
    scanf("%d %d", &m, &n);
    printf("Enter the elements of matrix : ");
    for(i = 0 ; i < m ; i++)
    for(j = 0 ; j < n ; j++)
    scanf("%d", &a[i][j]);
    for(i = 0 ; i < m ; i++)
    for(j = 0 ; j < n ; j++)
    sum = sum + a[i][j];
    printf("Sum of elements of the matrix is %d", sum);
}
```

The program displays the following output

```
Enter the order of matrix : 2 2
Enter the elements of matrix : 1 1 1 1
Sum of elements of the matrix is 4
```

In Program 1.16 we have used an array "a" and assigned 4 (4x2) elements of type int. The program displays the values and addresses of the memory occupied by the elements of the array matrix. Since the array is of type int each element in the array occupies 2 bytes of memory.

### Initializing an array using loops

An array can be initialized by using a for loop, a while loop or a do-while loop. The following examples illustrate the use of initializing an array using for loops.

### Examples for initializing an array using a for loop

- 1.
  ```
  int i, j, x = 5, mark[10][5];
  for(i = 0 ; i < 10 ; i++)
  for(j = 0 ; j < 5 ; j++)
  {
  mark[i][j] = x;
  x += 5;
  }
  ```

- 2.
  ```
  int i, j, mark[10][5];
  for(i = 0 ; i < 10 ; i++)
  for(j = 0 ; j < 5 ; j++)
  scanf("%d", &mark[i][j]);
  ```

In the first example, the for loop initializes the value 5 to the variable mark[0][0], 10 to the variable mark[0][1] and so on. In the second example, the scanf() function reads values from the user for the array. Similarly, arrays can also be initialized using while loop and do-while loops.

