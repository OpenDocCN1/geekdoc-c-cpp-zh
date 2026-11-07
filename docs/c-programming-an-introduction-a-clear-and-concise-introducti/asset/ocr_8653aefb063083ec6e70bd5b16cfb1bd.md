```
```cpp
dim temps[2][7] = {{87, 85, 89, 92, 94, 88, 90},
                   {79, 86, 85, 88, 93, 91}};
```
```

# Initializing a Two-Dimensional Array

To initialize a two-dimensional array, you have to write a nested for loop that traverses both the rows and the columns. Here is an example:

```
```cpp
const int rows = 2;
const int cols = 3;
int numbers[rows][cols];
    for(int r = 0; r < rows; ++r)
        for(int c = 0; c < cols; ++c)
            numbers[r][c] = 0;
```
```

In the code fragment above, the outer for loop is controlling the rows and the inner for loop is controlling the columns. So, the code starts with row 0 and populates columns 0, 1, and 2 with the value 0 and then moves to row 1, populating columns 0, 1, and 2 with the value 0 also.

# Displaying Two-Dimensional Array Elements

We can display the contents of the two-dimensional array above using the same nested for loop technique we used to initialize it. Here is our first try at it:

```
```cpp
for(int r = 0; r < rows; ++r)
    for (int c = 0; c < cols; ++c)
        cout << numbers[r][c] << " ";
```
```