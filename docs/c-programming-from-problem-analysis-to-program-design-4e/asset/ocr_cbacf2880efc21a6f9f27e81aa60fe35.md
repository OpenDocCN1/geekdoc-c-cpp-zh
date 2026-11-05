You can also get the upper bounds index using another Array class member. With the array dimensioned as

```
int [ , ] calories = new int [7, 3];
```

the last element (1700) is located at calories[6, 2]. Thus, the upper bound for the row is 6. The upper bound for the column is 2. The lower bound is 0 for both dimensions.

```
Console.WriteLine(calories.GetUpperBound(0)); // Returns 6 (row index)
```

> > **NOTE**
> The methods GetUpperBound( ) and GetLowerBound( ) return the upper or lower bounds of the specified dimension. Thus, GetUpperBound(1) returns 2 because the array is dimensioned to have three columns, so the largest index that could be used for the column is 2—the upper bound index for the column.

The foreach loop structure can be used to iterate through a two-dimensional array. Using the same format as noted previously, an identifier of the base type is defined. To display each of the values from the two-dimensional array, a foreach loop could be used as shown in Example 8-3.

# EXAMPLE 8.3

```
foreach (int cal in calories)
    Console.Write(cal + " ");
```

The output produced from Example 8-3 is in row major format—meaning every element in row 0 is printed before any element from row 1, as follows:

900 750 1020 300 1000 2700 500 700 2100 400 900 1780 600 1200
1100 575 1150 1900 600 1020 1700

> > **NOTE**
> You do not get the whole collection printed if you type Console.Write(calories); instead, the ToString( ) method of the object class is called. ToString( ) is defined in the object class to return an object's type. Thus, you would get System.Int32[ ] printed if you typed Console.Write(calories).

The foreach loop is used for read-only access. To change values, you need a different loop with two indexes. Example 8-4 illustrates how you traverse through the array clearing the contents from each cell.

# EXAMPLE 8.4

```
for (int r = 0; r < calories.GetLength(0); r++)
    for (int c = 0; c < calories.GetLength(1); c++)
        calories[r, c] = 0;
```