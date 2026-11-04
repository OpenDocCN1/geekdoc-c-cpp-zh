Here's an example where you have an array of integer values. You want to retrieve all the odd numbers in the array and sort them in descending order (that is, the bigger numbers come before the smaller numbers). Using LINQ, your code looks like this:

```
```csharp
int[] nums = { 12, 34, 10, 3, 45, 6, 90, 22, 87, 49, 13, 32 };
var oddNums = from n in nums
              where (n % 2 == 1)
              orderby n descending
              select n;
foreach (int n in oddNums)
    Console.WriteLine(n);
```
```

And here's what the code will print out:

```
```
87
49
45
13
3
```
```

To find out the total number of odd numbers found by the query, you can use the `Count()` method from the `oddNums` variable (of type `IEnumerable<int>`):

```
```csharp
int count = oddNums.Count();
```
```

You can also convert the result into an int array, like this:

```
```csharp
int[] oddNumsArray = oddNums.ToArray();
```
```

# ## Query Syntax versus Method Syntax and Lambda Expressions

The two LINQ queries in the previous section use the *query syntax*, which is written in a declarative manner, like this:

```
```csharp
var oddNums = from n in nums
              where (n % 2 == 1)
              orderby n descending
              select n;
```
```

In addition to using the query syntax, you can also use the *method syntax*, which is written using method calls like `Where` and `Select`, like this:

```
```csharp
int[] nums = { 12, 34, 10, 3, 45, 6, 90, 22, 87, 49, 13, 32 };
IEnumerable<int> oddNums = nums.Where(n => n % 2 == 1).OrderByDescending(n => n);
```
```

To find the total number of odd numbers in the array, you can also use the method syntax to query the array directly, like this:

```
```csharp
int count = (nums.Where(n => n % 2 == 1).OrderBy(n => n)).Count();
```
```