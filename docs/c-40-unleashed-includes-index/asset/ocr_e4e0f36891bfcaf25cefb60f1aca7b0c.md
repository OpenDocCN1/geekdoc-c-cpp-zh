less. In Visual Basic, you can omit the Select clause if it's trivial, but to maintain the source-hiding property, the compiler will inject the identity projection Select call:

```
Dim res = From n In nums
```

If there's more than only a trivial select clause (for example, a filter preceding it), a trivial select clause is compiled away, though. The reason is that the preceding operators, like a where clause, already cause the source to get hidden:

```
var res = from n in nums
    where n % 2 == 0
    select n;
```

In C#, the user is still required to write the select clause, but this time it gets dropped at compile time, resulting in the following code:

```
var res = nums.Where(n => n % 2 == 0);
```

This illustrates how syntactical differences across C# and Visual Basic maintain the (subtle) desired behavior of trivial projections when needed.

Stand-alone identity projections are not very useful other than for their source-hiding properties. But because C# requires you to write a select clause (or a group by clause) to terminate a query expression, you'll encounter identity projections quite often:

```
var res = from n in nums
    where n % 2 == 0
    select n;
```

# Nontrivial Projections

Of more interest are the nontrivial projections that really transform elements from the input sequences into some result, possibly of another type. A simple example is shown here:

```
var twice = from n in nums
    select n * 2;
```

The output of this query is an IEnumerable<int> whose produced elements contain the original elements each multiplied by two. Internally, this translates into a Select method call, as shown before, that looks like this:

```
var twice = nums.Select(n => n * 2);
```

In other words, Select takes in a function to execute on all the source's elements, giving back the output objects. The syntactical translation carried out by the compiler for a select clause is shown in Figure 19.12. We'll ignore the case where multiple range identifiers are “in scope” for the time being.