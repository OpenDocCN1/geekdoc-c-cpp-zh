```
    values[0, 2] = 0 * 2;
    ...
    values[1, 1] = 1 * 1;
    values[1, 2] = 1 * 2;
    ...
    values[4, 7] = 4 * 7;
```

The following code shows the C# syntax for quickly defining and initializing a two-dimensional array:

```
    int[,] cell =
    {
        {0, 1, 2},
        {3, 4, 5},
        {6, 7, 8},
    };
```

This syntax basically assigns the array variable equal to an array containing one-dimensional arrays of values.

> > **NOTE** Notice that the definition of the array’s final row of data ends with a comma. You don’t need this comma because nothing follows this last row, but C# allows you to include it to give the rows a more uniform format. The commas after the other rows are required because more rows follow them.

You can use similar syntax to make and initialize higher-dimensional arrays, although they’re harder to visualize graphically. For example, the following code makes a four-dimensional array of strings:

```
    string[, , ,] employeeData = new string[10, 20, 30, 40];
```

# ## Array Properties and Methods

All arrays have a `Length` property that your code can use to determine the number of items in the array. Arrays all have lower bound 0, so for one-dimensional arrays, `Length - 1` gives an array’s upper bound.

Arrays also have `GetLowerBound` and `GetUpperBound` methods that return the lower and upper bounds for a particular dimension in an array.

For example, the following code creates a 5-by-10 two-dimensional array. It then displays the lower and upper bounds for the first dimension. (Like an array’s indexes, the dimension numbers start at 0.)

```
    int[,] x = new int[5, 10];
    MessageBox.Show("The first dimension runs from " +
        x.GetLowerBound(0) + " to " + x.GetUpperBound(0));
```

The `Array` class also provides several useful static methods that you can use to manipulate arrays. For example, the following code sorts the array named `salaries`:

```
    Array.Sort(salaries);
```