# Chapter 14: Language Integrated Query (LINQ)

LINQ supports the following standard aggregate functions:

| Aggregate function | Description |
|---|---|
| Aggregate | Performs a custom aggregation operation on the values of a collection. |
| Average | Calculates the average value of a collection of values. |
| Count | Counts the elements in a collection, optionally only those elements that satisfy a predicate function. |
| LongCount | Counts the elements in a large collection, optionally only those elements that satisfy a predicate function. |
| Max | Determines the maximum value in a collection. |
| Min | Determines the minimum value in a collection. |
| Sum | Calculates the sum of the values in a collection. |

For example, the following statements print out the largest odd number contained in the nums array:

```
int[] nums = { 12, 34, 10, 3, 45, 6, 90, 22, 87, 49, 13, 32 };
var maxOddNums = nums.Where
    (n => n % 2 == 1).OrderByDescending(n => n).Max();
Console.WriteLine("Largest odd number: {0}", maxOddNums); //---87---
```

The following statements print out the sum of all the odd numbers in nums:

```
int[] nums = { 12, 34, 10, 3, 45, 6, 90, 22, 87, 49, 13, 32 };
var sumOfOddNums = nums.Where
    (n => n % 2 == 1).OrderByDescending(n => n).Sum();
Console.WriteLine("Sum of all odd number: {0}", sumOfOddNums); //---197---
```

# Joining Tables

So far you’ve been dealing with a single table. In real life, you often have multiple, related tables. A good example is the Northwind sample database, which contains a number of related tables, three of which are shown in Figure 14-7.

![](bbox=[0.28, 0.95, 0.85, 0.99])

Figure 14-7