A jagged array cannot be completely created with a single array-creation expression.
The following statement is a syntax error:

```
    int[][] c = new int[2][5]; // error
```

Instead, each one-dimensional array in the jagged array must be initialized separately.
A jagged array can be created as follows:

```
    int[][] c;
    c = new int[2][]; // create 2 rows
    c[0] = new int[5]; // create 5 columns for row 0
    c[1] = new int[3]; // create 3 columns for row 1
```

The preceding statements create a jagged array with two rows. Row 0 has five columns,
and row 1 has three columns.

# ### 8.9.3 Two-Dimensional Array Example: Displaying Element Values

Figure 8.19 demonstrates initializing rectangular and jagged arrays with array initializers and
using nested *for* loops to traverse the arrays (i.e., visit every element of each array). Class
`InitArray`'s `Main` method creates two arrays. Line 12 uses nested array initializers to ini-
tialize variable `rectangular` with an array in which row 0 has the values 1, 2 and 3, and
row 1 has the values 4, 5 and 6. Lines 17–19 used nested initializers of different lengths to
initialize variable `jagged`. In this case, the initializer uses the keyword `new` to create a one-
dimensional array for each row. Row 0 is initialized to have two elements with values 1
and 2, respectively. Row 1 is initialized to have one element with value 3. Row 2 is initial-
ized to have three elements with the values 4, 5 and 6, respectively.

```
    1 // Fig. 8.19: InitArray.cs
    2 // Initializing rectangular and jagged arrays.
    3 using System;
    4
    5 class InitArray
    6 {
    7    // create and output rectangular and jagged arrays
    8    static void Main()
    9    {
    10      // with rectangular arrays,
    11      // every row must be the same length.
    12      int[,] rectangular = {{1, 2, 3}, {4, 5, 6}};
    13
    14      // with jagged arrays,
    15      // we need to use "new int[]" for every row,
    16      // but every row does not need to be the same length.
    17      int[][] jagged = {new int[] {1, 2},
    18                        new int[] {3},
    19                        new int[] {4, 5, 6}};
    20
    21      OutputArray(rectangular); // displays array rectangular by row
    22      Console.WriteLine(); // output a blank line
    23      OutputArray(jagged); // displays array jagged by row
    24    }
```

**Fig. 8.19** Initializing jagged and rectangular arrays. (Part 1 of 2.)