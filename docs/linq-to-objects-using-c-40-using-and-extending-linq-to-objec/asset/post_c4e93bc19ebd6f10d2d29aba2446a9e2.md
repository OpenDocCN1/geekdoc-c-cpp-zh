
## 214 CHAPTER 7 EXTENDING LINQ TO OBJECTS

```csharp
return TakeRangeIterator<T>(
    source, b => true, endPredicate);
public static I IEnumerable<T> TakeRange<T>(
    IEnumerable<T> source,
    Func<T, bool> startPredicate,
    Func<T, bool> endPredicate)
{
    return TakeRangeIterator<T>(
    source, startPredicate, endPredicate);
}
```

To ensure a custom operator works as expected and stays that way in future releases, a solid set of unit tests should be written. To test the TakeRange operator and to demonstrate its basic usage, Listing 7-9 shows the minimum set of unit tests to prove the operator is functional. These tests confirm the following conditions when calling this operator:

- The operator works consistently with normal inputs. (It actually works!)
- The operator works consistently at the boundaries. (How does it handle the first or last element in the source?)
- The operator throws an exception when called from a null source sequence.
- The operator throws an exception if called with null predicates.

**Listing 7-9** The following unit tests are a starting point for testing the *TakeRange* operator

```csharp
[Test]
[ExpectedException("System.ArgumentNullException")]
public void NullSourceTest()
{
    int[] values = null;
    var result = values.TakeRange(
    start => true, end => true).ToArray<int>();
}
```

```csharp
[Test]
[ExpectedException("System.ArgumentNullException")]
public void NullStartPredicateTest()
{
    int[] values = null;
    int[] result = values.TakeRange(
        null, b => true).ToArray<int>();
}
```

```csharp
[Test]
[ExpectedException("System.ArgumentNullException")]
public void NullEndPredicateTest()
{
    int[] values = null;
    int[] result = values.TakeRange(
        a => true, null).ToArray<int>();
}
```

```csharp
[Test]
public void IntArrayTest()
{
    var values = Enumerable.Range(0, 20);

    int[] result = values.TakeRange(
        start => start > 4,
        end => end > 9).ToArray<int>();

    Assert.AreEqual(
        5, result.Count(), "incorrect count returned");

    // expecting 5,6,7,8,9 to be returned
    for (int i = 0; i < result.Count(); i++)
        Assert.AreEqual(i + 5, result[i]);
}
```

```csharp
[Test]
public void IntArrayEndPredicateOnlyTest()
{
    var values = Enumerable.Range(0, 20);

    int[] result = values.TakeRange(
        end => end > 9).ToArray<int>();

    Assert.AreEqual(
        10, result.Count(), "incorrect count returned");

    // expecting 10-19 to be returned
    for (int i = 10; i < result.Count(); i++)
        Assert.AreEqual(i, result[i]);
}
```

Following are a few tips for developing new sequence operators:

- Separate the iterator code from the extension method functions so you can provide many overloads that allow optional input arguments all calling the same main method function.
- Test input arguments for null values and throw an ArgumentNullException("arg"); if these input arguments are essential for correct operation.
- Follow the same patterns and error handling that Microsoft used in their operators. (I've followed as many as possible throughout this book.)

# Writing an Aggregate Operator

The role of an aggregate operator is to traverse a source sequence and carry out a function (often arithmetic) on the elements. Example aggregate standard query operators are Sum, Min, and Max, which return the sum of values, the smallest value, and the largest value, respectively.

# The Min Operator

To understand the basics of an aggregate style operator, let's look at the implementation of the Min standard query operator. Listing 7-10 shows the error handling and functional code to find the minimum integer in a sequence.

Listing 7-10 Implementation of the Min standard query operator

```csharp
public static int Min(
    IEnumerable<int> source)
{
    if (source == null)
        throw new ArgumentNullException("source");

    int num = 0;
    bool flag = false;
    foreach (int num2 in source)
    {
        if (flag)
        {
            if (num2 < num)
                num = num2;
        }
        else
        {
            num = num2;
            flag = true;
        }
    }

    if (!flag)
        throw new
        InvalidOperationException("No elements");

    return num;
}
```

Listing 7-10 first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

## 214 CHAPTER 7 EXTENDING LINQ TO OBJECTS

The role of an aggregate operator is to traverse a source sequence and carry out a function (often arithmetic) on the elements. Example aggregate standard query operators are Sum, Min, and Max, which return the sum of values, the smallest value, and the largest value, respectively.

# The Min Operator

To understand the basics of an aggregate style operator, let's look at the implementation of the Min standard query operator. Listing 7-10 shows the error handling and functional code to find the minimum integer in a sequence.

Listing 7-10 Implementation of the Min standard query operator

```csharp
public static int Min(
    IEnumerable<int> source)
{
    if (source == null)
        throw new ArgumentNullException("source");

    int num = 0;
    bool flag = false;
    foreach (int num2 in source)
    {
        if (flag)
        {
            if (num2 < num)
                num = num2;
        }
        else
        {
            num = num2;
            flag = true;
        }
    }

    if (!flag)
        throw new
        InvalidOperationException("No elements");

    return num;
}
```

Listing 7-10 first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The role of an aggregate operator is to traverse a source sequence and carry out a function (often arithmetic) on the elements. Example aggregate standard query operators are Sum, Min, and Max, which return the sum of values, the smallest value, and the largest value, respectively.

# The Min Operator

To understand the basics of an aggregate style operator, let's look at the implementation of the Min standard query operator. Listing 7-10 shows the error handling and functional code to find the minimum integer in a sequence.

Listing 7-10 Implementation of the Min standard query operator

```csharp
public static int Min(
    IEnumerable<int> source)
{
    if (source == null)
        throw new ArgumentNullException("source");

    int num = 0;
    bool flag = false;
    foreach (int num2 in source)
    {
        if (flag)
        {
            if (num2 < num)
                num = num2;
        }
        else
        {
            num = num2;
            flag = true;
        }
    }

    if (!flag)
        throw new
        InvalidOperationException("No elements");

    return num;
}
```

Listing 7-10 first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The code shown previously first checks the source sequence for a null condition and throws an exception if that is the case. If the source sequence is not null, each element is compared to the current minimum element found so far (by value), except the first element. When flag is false, the first element hasn't been evaluated, and if the sequence is empty (no first element ever), an InvalidOperationException is thrown; otherwise, the first element's value is assigned to the current minimum variable on the first iteration step. After iterating and testing each element's value against the current minimum found, the lowest value is returned.

The role of an aggregate operator is to traverse a source sequence and carry out a function (often arithmetic) on the elements. Example aggregate standard query operators are Sum, Min, and Max, which return the sum of values, the smallest value, and the largest value, respectively.

# Building the Long Operator

Early on when working with LINQ to Objects I found the built-in Sum operator that sums the values for a set of integer returned the result as an integer. This didn't suit my requirements, and sequences quickly overflowed the integer maximum of the return type. A custom operator was needed to return the arithmetic sum of integer values with a result type of long (overloading the built-in min operators) didn't solve the issue. Because I was only changing the return type and not an argument, C# compiler's overload resolution was satisfied—hence the LongSum).
The LongSum operator has the following requirements:

- Take an input IEnumerable<int> collection as a source and return the arithmetic sum as type long.
- Follow the signature pattern of the existing Sum operators. Create two extension method overloaded signatures, one that takes a selector expression and that doesn't.
- Throw an ArgumentNullException if the source sequence is null.
- If the source sequence is empty, return a result of zero.

The overall goal is to make the new LongSum extension method identical to using the Sum extension methods. 7-12 shows the full code for implementing the LongSum operator. The code iterates the source collection using a foreach loop and simply sums the element values as it go. A Selector expression argument is passed into the operator, that Selector expression is first evaluated before calling the other LongSum overload with simply a source sequence of integer values.

**Listing 7-12** The code for the LongSum operator, which takes a sequence of int values and returns the mathematical sum up to the maximum value allowed in a Long type

```csharp
public static long LongSum(
  this IEnumerable<int> source)
{
  if (source == null)
    throw new ArgumentNullException("source");

  long sum = 0;
}
```
