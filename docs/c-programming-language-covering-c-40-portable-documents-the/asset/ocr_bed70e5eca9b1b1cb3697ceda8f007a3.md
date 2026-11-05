The order in which foreach traverses the elements of an array is as follows: For single-dimensional arrays, elements are traversed in increasing index order, starting with index 0 and ending with index Length - 1. For multi-dimensional arrays, elements are traversed such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.

The following example prints out each value in a two-dimensional array, in element order:

```
using System;
class Test
{
    static void Main()
    {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };
        foreach (double elementValue in values)
            Console.Write("{0} ", elementValue);
        Console.WriteLine();
    }
}
```

The output produced is as follows:

1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9

In the example
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
the type of n is inferred to be int, the element type of numbers.

# 8.9 Jump Statements

Jump statements unconditionally transfer control.

+   jump-statement:
+     break-statement
+     continue-statement
+     goto-statement
+     return-statement
+     throw-statement