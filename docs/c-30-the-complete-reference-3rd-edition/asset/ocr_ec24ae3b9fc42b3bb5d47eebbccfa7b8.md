The minimum value is 1
The maximum value is 5
The first value is 3
The last value is 4
The sum is 15
The average is 3
All values are greater than zero.
At least one value is even.
The array contains 3.

You can also use the query-related extension methods within a query based on the C# query syntax. In fact, it is quite common to do so. For example, this program uses Average() to obtain a sequence that contains only those values that are less than the average of the values in an array.

```
// Use Average() with the query syntax.
using System;
using System.Linq;

class ExtMethods2 {
    static void Main() {
        int[] nums = { 1, 2, 4, 8, 6, 9, 10, 3, 6, 7 };
        var ltAvg = from n in nums
                    let x = nums.Average()
                    where n < x
                    select n;
        Console.WriteLine("The average is " + nums.Average());
        Console.Write("These values are less than the average: ");
        // Execute the query and display the results.
        foreach(int i in ltAvg) Console.Write(i + " ");
        Console.WriteLine();
    }
}
```

The output is shown here:

The average is 5.6
These values are less than the average: 1 2 4 3

Pay special attention to the query:

```
var ltAvg = from n in nums
            let x = nums.Average()
            where n < x
            select n;
```

Notice in the let statement, x is set equal to the average of the values in nums. This value is obtained by calling Average() on nums.