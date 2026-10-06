# 222 CHAPTER 7 EXTENDING LINQ TO OBJECTS

Listing 7-11 for the Min operator as a good starting list for your operators.

+   Provide an overload for each operator that takes a selector expression. Aggregate functions are often used in the select project of a grouped query result, where you want to define the numeric sequence you want aggregated. To implement these over, call the Select standard query operator passing in the select argument before calling your custom operator, for example:
```csharp
return
    .Select(selector)
    .LongSum();
```

+   Look at the source code for the standard query operators by using Red Gate Reflector (http://www.red-gate.com/products/reflector/). Follow the same patterns and error handling that Microsoft uses in their operators.

+   Test input arguments for null values and throwNullException("arg"); if these input arguments are essential for correct operation.

# Writing a Grouping Operator

Grouping operators return collections of the source elements (variations thereof) grouped by some algorithm. Examples of grouping operators from the standard query operators are GroupBy and Lookup.

The general steps for building a new grouping operator are:

+   Write an IGrouping<TKey, TElement> list implementation to hold your groups. type implementation, however it is marked as internal. I recommend copying it as a template for your own grouping list implementation (which is what I did in this example, and provided in Listing 7-14).

+   Write an enumeration method that builds the groups and yields the grouped results using instances of the IGrouping<TKey, TElement> types.

+   Write an extension method signature(s) and implement each method by calling the enumeration method with the appropriate arguments.