# Memory Layout

The subscripts in the definition of a two-dimensional array represent rows and columns. This format maps the way that data elements are laid out in the memory. The elements of all arrays are stored contiguously in increasing memory locations, essentially in a single list. If we consider the memory as a row of bytes, with the lowest address on the left and the highest address on the right, a simple array will be stored in memory with the first element at the left end and the last element at the right end. Similarly, a two-dimensional array is stored 'row-wise', starting from the first row and ending with the last row, treating each row like a simple array. This is illustrated below.

![](bbox=[0.25, 0.3, 0.9, 0.57])

# Memory Layout

For a multi-dimensional array, the order of storage is that the first element stored has 0 in all its subscripts, the second has all of its subscripts 0 except the far right which has a value of 1 and so on. The elements of a 2 x 3 x 3 array will be stored as under

![](bbox=[0.28, 0.72, 0.92, 0.86])

The far right subscript increments first and the other subscripts increment in order from right to left. The sequence numbers 1, 2, ......, 18 represents the location of that element in the list

# 3.7 MULTI-DIMENSIONAL ARRAYS

C allows arrays of three or more dimensions. The exact limit is determined by the compiler. The general form of a multi-dimensional array is

```
type array_name[s1][s2][s3]....[sm];
```

where s_i is the size of the ith dimension. Some examples are:

```
int survey[3][5][12];
float table[5][4][5][3];
```

survey is a three-dimensional array declared to contain 180 integer type elements. Similarly table is a four-dimensional array containing 300 elements of floating-point type.

The array survey may represent a survey data of rainfall during the last three years from January to December in five cities.

If the first index denotes year, the second city and the third month, then the element survey[2][3][10] denotes the rainfall in the month of October during the second year in city-3.