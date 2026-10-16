
7. When using vectors of vectors, leave a space between the two > symbols. A common mistake is to forget this and to declare a vector of vectors with a statement like

```
vector<vector<int>> myGrid;
```

The compiler will read the >> as the input (or right-shift) operator, and because this makes no sense in this context, a compilation error will result. The correct approach is to leave a space:

```
vector<vector<int> > myGrid;
```

8. When processing the elements of a multidimensional array/vector using nested loops, the loops must be arranged so that the indices vary in the appropriate order. To illustrate, suppose that the two-dimensional array table is declared by

```
typedef int Array3x4 [3] [4];
Array3x4 table;
```

and the following data values are to be read into the array:

```
11 22 27 35 39 40 48 51 57 66 67 92
```

If these values are to be read and assigned in a row-wise manner so that the value is the matrix

```
11    22    27    35
39    40    48    51
57    66    67    92
```

then the following nested for loops are appropriate:

```
for (int row = 0; row < 3; row++)
    for (int col = 0; col < 4; col++)
        cin >> table[row][col];
```

If the order of these loops is reversed,

```
for (int col = 0; col < 4; col++)
    for (int row = 0; row < 3; row++)
        cin >> table[row][col];
```

then table will be loaded column-by-column, instead of row-by-row,

```
11  35  48  66
22  39  51  67
27  40  57  92
```

and operations applied to table will produce incorrect results.

## TEST YOURSELF

### Section 13.2

- 1. A(n) ______ array is useful for storing data arranged in rows and columns.
- 2. A(n) ______ array is useful for storing data arranged in rows, columns, and ranks.
- 3. Arrays with the same number of rows as columns are said to be ______ arrays.

Questions 4–14 refer to the following two-dimensional array:

mat:
[0] [1] [2] [3]
[0] 11 22 0 43
[1] 1 -1 0 999
[2] -5 39 15 82
[3] 1 2 3 4
[4] 44 33 22 11

Find the value of each expression in Questions 4–9.

- 4. mat[2][3]
- 5. mat[4][1]
- 6. mat[1][1]
- 7. mat[0][0] + mat[0][1]
- 8. mat[0][0] + mat[1][0]
- 9. mat[3]

Find the value of x in each of Questions 10–14.

```
10. int x = 0;
    for (int i = 0; i <= 4; i++)
        x += mat[i][1];
```

```
11. int x = 0;
    for (int j = 0; j < 4; j++)
        x += mat[1][j];
```

```
12. int x = 0;
    for (int k = 0; k <= 3; k++)
        x += mat[k][k];
```

4. Write an expression to change the element in the second row and third column of grid to 1.1.

5. What is the value of grid.size()?

6. What is the value of grid[0].size()?

7. Write a statement to append the value 99.9 at the end of the second row of grid.

8. Write statements to append a row containing 4 zeros at the bottom of grid.

## EXERCISES

### Section 13.2

Exercises 1–6 assume that the following declarations have been made:

```
const int NUM_SIZES = 6;
typedef bool BitArray[2][2][2];
typedef int Device[NUM_SIZES][10][20];
typedef Thingamajig Device[5];
```

How many elements can be stored in an array of each type?

- 1. int[50][100]
- 2. char[26][26]
- 3. bool[2][2][2]
- 4. BitArray
- 5. Device
- 6. Thingamajig

Exercises 7–10 assume that the following declarations have been made:

```
typedef int Array3x3 [3][3];
Array3X3 mat;
```

Tell what value (if any) is assigned to each array element, or explain why an error occurs.

```
7. for (int i = 0; i < 3; i++)
    for (int j = 0; j < 3; j++)
        mat[i][j] = i + j;
```

```
8. for (int i = 0; i < 3; i++)
    for (int j = 2; j >= 0; j--)
        if (i == j)
            mat[i][j] = 0;
```

```
else
mat[i][j] = 1;
```

```
9. for (int i = 0; i < 3; i++)
for (int j = 0; j < 3; j++)
if (i < j)
mat[i][j] = -1
else if (i == j)
mat[i][j] = 0;
else
mat[i][j] = 1;
```

```
10. for (int i = 0; i < 3; i++)
{
for (int j = 0; j < i; j++)
mat[i][j] = 0;
for (j = i; j < 3; j++)
mat[i][j] = 2
}
```

Exercises 11-14 assume that the following declaration has been made:

```
char logo[2][10] = {"Nuts", "and Bolts"};
```

Tell what output will be produced or explain why an error occurs.

```
for (int i = 0; i < 2; i++)
{
for (int j = 0; j < 9; j++)
cout << logo[i][j];
cout << endl;
}
```

```
for (int j = 0; j < 9; j++)
{
for (int i = 0; i < 2; i++)
cout << logo[i][j];
cout << endl;
}
```

```
for (int i = 0; i < 2; i++)
{
for (int j = 0; j < 9; j++)
cout << logo[j][i];
cout << endl;
}
```

14. for (int i = 0; i < 2; i++)
{
    for (int j = 8; j >= 0; j--)
        cout << logo[i][j];
    cout << endl;
}

15. Write a function that, given a TableOfTemperatures (as declared in this section), will calculate and return the average temperature at each of the three locations.

16. Like one-dimensional arrays, multidimensional arrays are stored in a block of consecutive memory locations, and address translation formulas are used to determine the location in memory of each array element. To illustrate, consider a 3 × 4 array a of integers, and assume that an integer can be stored in one memory word. If a is allocated memory in a row-wise manner and b is its base address, then the first row of a—a[0][0], a[0][1], a[0][2], a[0][3]—is stored in words b, b + 1, b + 2, b + 3; the second row in words b + 4 through b + 7; and the third row in words b + 8 through b + 11.

| Address | Memory | Array Element |
|---|---|---|
|  | ⋮ |  |
| b |  | a[0][0] |
| b + 1 |  | a[0][1] |
| b + 2 |  | a[0][2] |
| b + 3 |  | a[0][3] |
| b + 4 |  | a[1][0] |
| b + 5 |  | a[1][1] |
| b + 6 |  | a[1][2] |
| b + 7 |  | a[1][3] |
| b + 8 |  | a[2][0] |
| b + 9 |  | a[2][1] |
| b + 10 |  | a[2][2] |
| b + 11 |  | a[2][3] |
|  | ⋮ |  |

In general, a[i][j] is stored in word b + 4i + j.

- a. Give a similar diagram and formula if a is a 3 × 3 array of integer values.
- b. Give a similar diagram and formula if a is a 3 × 4 array of double values, where double values require two words for storage.

## PROGRAMMING PROBLEMS

Sections 13.1–13.2

1. Write a program to calculate and display the first ten rows of Pascal’s triangle. The first part of the triangle has the form

1
1 1
1 2 1
1 3 3 1
1 4 6 4 1

in which each row begins and ends with 1, and each of the other entries in a row is the sum of the two entries just above it. If this form for the output seems too challenging, you might display the triangle as

1
1 1
1 2 1
1 3 3 1
1 4 6 4 1

2. A demographic study of the metropolitan area around Dogpatch divided it into three regions: urban, suburban, and exurban, and published the following table showing the annual migration from one region to another (the numbers represent percentages):

| ↷ | Urban | Suburban | Exurban |
|---|---|---|---|
| Urban | 1.1 | 0.3 | 0.7 |
| Suburban | 0.1 | 1.2 | 0.3 |
| Exurban | 0.2 | 0.6 | 1.3 |

For example, 0.3 percent of the urbanites (0.003 times the current population) move to the suburbs each year. The diagonal entries represent internal growth rates. Using a two-dimensional array to store this table, write a program to determine the population of each region after 10, 20, 30, 40, and 50 years. Assume that the current populations of the urban, suburban, and exurban regions are 2.1, 1.4, and 0.9 million, respectively.

3. The famous mathematician G. H. Hardy once mentioned to the brilliant young Indian mathematician Ramanujan that he had just ridden in a taxi whose number he considered to be very dull. Ramanujan promptly replied that, on the contrary, the number was very interesting because it was the smallest positive integer that could be written as the sum of two cubes (that is, written in the form x³ + y³, with x and y integers) in two different ways. Write a program to find the number of Hardy’s taxi.

4. An engineer has a file containing a table of ratings for various products being tested, where the first line of the file contains the number of products and the number of times each was tested; each row of the table represents the ratings for a given product and each column represents the rating on a given test run. The maximum possible rating was 100 points. Write a program that, given the name of such a file, generates a report summarizing the overall average rating for each product and the average rating on each test run.
