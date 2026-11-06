We have declared and initialized out jagged array in the above code. The code will give you the following result:

```
1
3
6
```

A jagged array can also store a multidimensional array as a value. We can use [,] in the second bracket to indicate a multi-dimensional. Here is an example:

```
```csharp
using System;

public class MyArray
{
    public static void Main()
    {
        int[][,] jaggedArray = new int[3][,];

        jaggedArray[0] = new int[3, 2] { { 1, 5 }, { 2, 6 }, { 4, 8 } };
        jaggedArray[1] = new int[2, 2] { { 3, 5 }, { 4, 6 } };
        jaggedArray[2] = new int[2, 2];

        Console.WriteLine(jaggedArray[0][1,1]);
        Console.WriteLine(jaggedArray[1][1,0]);

        Console.WriteLine(jaggedArray[1][1,1]);
    }
}
```
```

The code will return the following:

```
6
4
6
```

In case an additional bracket is added, then this will become an array of array of array. This is demonstrated in the following example:

```
```csharp
using System;
```
```