Suppose you want to print all the array contents. In that case, you can use one for
loop to change rows and a nested, for loop to change columns:

```
for (int row = 0; row < 4; row++)
    for (int col = 0; col < 5; ++col)
        cout << maxtemps[row][col] << "\t";
    cout << endl;
```

For each value of row, the inner loop cycles through all the col values. This exam-
ple prints tab character (\v in C++ escape character) after each value and a
newline character after each complete row.

# Initializing a Two-Dimensional Array

When you create a two-dimensional array, you have the option of initializing each ele-
ment. The technique is based on that for initializing a one-dimensional array. Remember
that you do this by providing a comma-separated list of values enclosed in braces:

```
// initializing a one-dimensional array
int btus[5] = { 23, 26, 24, 31, 28 };
```

For a two-dimensional array, each element is itself an array, so you can initialize each
element using a form like that in the previous code example. Thus, the initialization
of a comma-separated series of one-dimensional initializations, all enclosed in the
set of braces:

```
int maxtemps[4][5] = // 2-D array
{
    {96, 100, 87, 101, 105}, // values for maxtemps[0]
    {96, 98, 101, 107, 104}, // values for maxtemps[1]
    {97, 101, 93, 108, 107}, // values for maxtemps[2]
    {98, 103, 95, 109, 108} // values for maxtemps[3]
};
```

You can visualize maxtemps as four rows of five numbers each. The term {94, 98,
87, 103, 101} initializes the first row, represented by maxtemps[0]. As a matter of style,
acing each row of data on its own line, if possible, makes the data easier to read.

# Using a Two-Dimensional Array

Listing 5.20 incorporates an initialized two-dimensional array and a nested loop into a
program. This time the program reverses the order of the loops, placing the column
(city index) on the outside and the row (year index) on the inside. Also it uses a