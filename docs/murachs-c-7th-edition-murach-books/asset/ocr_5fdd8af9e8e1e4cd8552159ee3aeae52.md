# The three stages of a query operation

+   1. Get the data source. If the data source is an array, for example, you must declare the array and then assign values to its elements.
+   2. Define the query.
+   3. Execute the query to return the results.

# A LINQ query that retrieves data from an array

# Code that defines the array

```
int[] numbers = new int[6];
for (int i = 0; i < numbers.Length; i++)
    numbers[i] = i;
```

# A statement that defines the query expression

```
var numberList = from number in numbers
    where number % 2 == 0
    orderby number descending
    select number;
```

# Code that executes the query

```
string numberDisplay = "";
foreach (var number in numberList)
    numberDisplay += number + "\t\t\n";
MessageBox.Show(numberDisplay, "Sorted Even Numbers");
```

![](bbox=[0.156, 0.465, 0.322, 0.594])

# Description

+   - The process described above is called *deferred execution* because the query isn’t executed when it’s defined. Instead, it’s executed when the application tries to access the individual elements returned by the query, such as when the query is used in a foreach statement.
+   - If a query isn’t executed when it’s defined, it’s stored in a *query variable*. In that case, the query variable is implicitly typed as IEnumerable<T> where T is the type of each element. In the example above, the numberList variable is assigned the type IEnumerable<int> since the numbers array contains integers.
+   - If a query requires access to the individual elements identified by the query expression, *immediate execution* occurs. In that case, the query expression isn’t saved in a query variable.