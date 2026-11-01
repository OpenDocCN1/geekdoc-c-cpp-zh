# TABLE 20-1: Aggregate Operators for Numeric Results

| OPERATOR | DESCRIPTION |
|---|---|
| Count() | Count of results |
| Min() | Minimum value in results |
| Max() | Maximum value in results |
| Average() | Average value of numeric results |
| Sum() | Total of all of numeric results |

There are more aggregate operators, such as Aggregate(), for executing arbitrary code in a manner that enables you to code your own aggregate function. However, those are for advanced users and therefore beyond the scope of this book.

> **NOTE** Because the aggregate operators return a simple scalar type instead of a sequence for their results, their use forces immediate execution of query results with no deferred execution.

In the following Try It Out, you modify the large-number query and use aggregate operators to explore the result set from the greater-than version of the large-number query using LINQ.

# TRY IT OUT Numeric Aggregate Operators: BegVCSharp_20_7_NumericAggregates\Program.cs

Follow these steps to create the example in Visual Studio 2015:

+   1. For this example, you can either modify the LargeNumberQuery example you just made or create a new console project named BegVCSharp_20_7_NumericAggregates in the directory C:\BegVCSharp\Chapter20.
+   2. As before, when you create the project, Visual Studio 2015 includes the Linq namespace method in Program.cs. You just need to modify the Main() method as shown in the following code and in the rest of this Try It Out. As with the previous example, the orderby clause is not used in this query. However, the condition on the where clause is the opposite of the previous example (the numbers are greater than 1,000 (n > 1000), instead of less than 1,000):

```
static void Main(string[] args)
{
    int[] numbers = GenerateLotsOfNumbers(12345678);
    WriteLine("Numeric Aggregates");
    var queryResults =
```