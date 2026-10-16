kept empty because every row has a different number of elements.\nNext, the element number of the rows can be set for every row:

```
int[][] jagged = new int[3][];
jagged[0] = new int[2] { 1, 2 };
jagged[1] = new int[6] { 3, 4, 5, 6, 7, 8 };
jagged[2] = new int[3] { 9, 10, 11 };
```

You can iterate through all the elements of a jagged array with nested `for` loops. In the outer `for` loop every row is iterated, and the inner `for` loop iterates through every element inside a row:

```
for (int row = 0; row < jagged.Length; row++)
{
    for (int element = 0; element < jagged[row].Length; element++)
    {
        WriteLine($"row: {row}, element: {element}, value: {jagged[row][element]}");
    }
}
```

The output of the iteration displays the rows and every element within the rows:

```
row: 0, element: 0, value: 1
row: 0, element: 1, value: 2
row: 1, element: 0, value: 3
row: 1, element: 1, value: 4
row: 1, element: 2, value: 5
row: 1, element: 3, value: 6
row: 1, element: 4, value: 7
row: 1, element: 5, value: 8
row: 2, element: 0, value: 9
row: 2, element: 1, value: 10
row: 2, element: 2, value: 11
```

# Array Class

Declaring an array with brackets is a C# notation using the `Array` class. Using the C# syntax behind the scenes creates a new class that derives from the abstract base class `Array`. This makes it possible to use methods and properties that are defined with the `Array` class with every C# array. For example, you’ve already used the `Length` property or iterated through the array by using the `foreach` statement. By doing this, you are using the `GetEnumerator` method of the `Array` class.

Other properties implemented by the `Array` class are `LongLength`, for arrays in which the number of items doesn’t fit within an integer, and `Rank`, to get the number of dimensions.

Let’s have a look at other members of the `Array` class by getting into various features.

# Creating Arrays

The `Array` class is abstract, so you cannot create an array by using a constructor. However, instead of using the C# syntax to create array