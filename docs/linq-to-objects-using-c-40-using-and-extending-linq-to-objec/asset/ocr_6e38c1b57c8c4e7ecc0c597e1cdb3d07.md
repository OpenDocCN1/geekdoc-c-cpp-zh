# 196 CHAPTER 7 EXTENDING LINQ TO OBJECTS

**Grouping operator**—Those that return groupings of elements from a sequence (GroupBy, GroupJoin).

This chapter looks at each type of operator in detail and constructs (and tests) a sample operator for each operator type.

# Writing a Single Element Operator

The role of a single element operator is to add an extension method to any type that implements IEnumerable<T> and return a single element from collection. The built-in standard query operators First, Last and ElementAt are examples of this category of operator, returning the first element, the last element, or the element at a given index position, respectively.

Understanding how Microsoft constructed the standard query operators is the first step to understanding how to write custom operators. To explore Microsoft's approach to operator construction, let's build our own version of the Last operator before moving onto building a more complex operator.

# Building Our Own Last Operator

To learn how to build an operator that returns a single element, let's first look at how the built-in standard query operator Last is implemented. The shortest-compilable implementation for the Last operator is shown in Listing 7-1.

**Listing 7-1** Shortest compilable Last operator implementation

```
public static T Last<T>(
    IEnumerable<T> source)
{
    using (IEnumerator<T> enumerator = source.GetEnumerator())
    {
        if (enumerator.MoveNext())
        {
            T current;
            do
            {
                current = enumerator.Current;
            }
            while (enumerator.MoveNext());
        }
    }
```