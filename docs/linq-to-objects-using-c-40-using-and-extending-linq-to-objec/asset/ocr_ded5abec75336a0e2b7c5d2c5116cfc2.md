# GENERATION OPERATORS—GENERATING SEQUENCES OF DATA 155

```
// order dependent
bool n12 = n1.SequenceEqual(n2);

// case-sensitive using the default comparer
bool n13 = n1.SequenceEqual(n3);

// passing in a comparer - this time using the
built-in StringComparer static instances.
bool n13_2 = n1.SequenceEqual(
n3, StringComparer.CurrentCultureIgnoreCase);

Console.WriteLine("n12 = {0}, n13 = {1}, n13_2 = {2}",
n12, n13, n13_2);
```

Output 5-11

n12 = False, n13 = False, n13_2 = True

# Generation Operators—Generating Sequences of Data

Generating sequences of data to combine with LINQ to Object queries is often necessary when building unit tests and when working with indexable data sources, like iterating through the x and y coordinates of a bitmap image. the generation methods are not extension methods; they are purely static method calls in the System.Linq.Enumerable class and are included with the LINQ operators because they fulfill the important task of creating sequences of data without using a for-loop construct.

# Empty Operator

The Empty operator doesn't appear very useful at first sight. So why return an empty IEnumerable<T> sequence? The main use for this operator is for testing the empty sequence error handling behavior of other operators.