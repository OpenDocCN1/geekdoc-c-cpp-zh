# Figure 11.12 A 2 x 3 two-dimensional array

![](bbox=[0.35, 0.18, 0.59, 0.34])

Listing 11.19 (resizearray.cpp) contains the code to perform this array resizing. A vector object manages a dynamic array, and its push_back method takes care these details for us.

# 11.2.5 Multidimensional Arrays

Just as C++ supports higher-dimensional vectors, it also supports multidimensional arrays. The following statement:

```
int a[2][3];
```

declares a to be a two-dimensional (2D) array of integers. In this case, the declaration specifies that array a contains two rows and three columns. Figure 11.12 shows the logical structure of the array created by the following sequence of code:

```
int a[2][3]; // a is a 2D array
a[0][0] = 5;
a[0][1] = 19;
a[0][2] = 3;
a[1][0] = 22;
a[1][1] = -8;
a[1][2] = 10;
```

The two-dimensional array a is said to be a 2 x 3 array, meaning it has two rows and three columns (as shown in Figure 11.12). Rows are arranged horizontally, and the values in columns are arranged vertically. In each of the assignment statements above, for example

```
a[1][0] = 22;
```

the first index (here 1) signifies the row and the second index (here 0) denotes the column of the element within the array.

Using a syntax similar to 2D vectors, we could have declared and created the 2D array above as:

```
int a[2][3] = { { 5, 19, 3 },
```