# NULLABLE TYPE SHORTHAND Starting with .NET Framework 2.0, it was possible to specify a value type variable declaration allowing a null value, a feature called nullable types. Earlier versions of .NET didn't support value types being null. To make it easier to define a value type as nullable, Microsoft added a shorthand way of declaring them, simply appending a question mark to the type. The following two lines both declare a nullable type of integer; the second (i2) uses the shorthand syntax:

```
Nullable<int> i1 = null;
int? i2 = null;
```

For each operator, in addition to the various overload types for different numeric input elements themselves, there is an overload that works on the sequence elements and takes a selector function to specify the values to be aggregated. The signatures for these operators follow a repetitive pattern, and the following example shows the Sum operator that returns a decimal value:

```
public static decimal Sum<TSource>(
    IEnumerable<TSource> source,
    Func<TSource, decimal> selector);
```

Aggregate operations using selector functions are often useful in queries that group data. Listing 5-4 demonstrates a fairly complex query that summarizes fictitious call log data. In this case, the query groups all incoming calls from the same number and then aggregates the total number of calls, call time, and average call time. This query generates the Console output shown in Output 5-3.

List 5-4 Aggregate operators are useful for generating summary data in a query that groups data—see Output 5-3

```
List<CallLog> callLog = CallLog.SampleData();

var q = from call in callLog
    where call.Incoming == true
    group call by call.Number into g
    select new {
```