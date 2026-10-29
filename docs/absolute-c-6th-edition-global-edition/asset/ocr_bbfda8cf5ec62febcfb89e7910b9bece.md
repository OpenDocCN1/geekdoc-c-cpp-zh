In C++, a two-dimensional array, such as page, is actually an array of arrays. The array type shown is actually a one-dimensional array of size 30, whose base type is a one-dimensional array of characters of size 100. Normally, this need not concern you, and you can usually act as if the array page were an array with two indexes (rather than an array of arrays, which is harder to keep track of). There is, however, at least one situation in which a two-dimensional array looks very much like an array of arrays, namely, when you have a function with an array parameter for a two-dimensional array, which is discussed in the next subsection.

# Multidimensional Array Declaration

**SYNTAX**

_Type Array_Name[Size_Dim_1][Size_Dim_2]...[Size_Dim_Last];_

**EXAMPLES**

```cpp
char page[30][100];
int matrix[2][3];
double threeD[Picture[10][20][30];
```

An array declaration of the form shown here will define one indexed variable for each combination of array indexes. For example, the second of the previous sample declarations defines the following six indexed variables for the array matrix:

```cpp
matrix[0][0], matrix[0][1], matrix[0][2],
matrix[1][0], matrix[1][1], matrix[1][2]
```

# Multidimensional Array Parameters

The following declaration of a two-dimensional array actually declares a one-dimensional array of size 30 whose base type is a one-dimensional array of characters of size 100:

```cpp
char page[30][100];
```

Viewing a two-dimensional array as an array of arrays will help you to understand how C++ handles parameters for multidimensional arrays.

For example, the following is a function that takes an array, like page, and prints it to the screen:

```
```cpp
void displayPage(const char p[][100], int sizeDimension1)
{
    for (int index1 = 0; index1 < sizeDimension1; index1++)
    {
        // Printing one line:
        for (int index2 = 0; index2 < 100; index2++)
            cout << p[index1][index2];
        cout << endl;
    }
}
```
```