![](bbox=[0.12, 0.1, 0.55, 0.28])

# FIGURE 7.13 Importing namespaces made easy.

It should be pretty clear what this query does: It finds all the processes running on the machine with a working set larger than 50MB. The 64 in the WorkingSet64 property name reflects the precision of the value (long, or Int64). Another 32-bit property called WorkingSet exists, which is now marked obsolete due to its insufficient range to deal with 64-bit processes that can have a working set that doesn't fit in a 32-bit value.

Where the need for implicitly typed local variables comes in is due to the select clause, in which we're using an anonymous type to project out only the pieces of data we're interested in: the process name and the working set in megabytes. We cover anonymous types when talking about LINQ more extensively in Chapters 19 and 20, but your gut feeling is right: If a type doesn't have a name (at least not pronounceable by the developer because the compiler has generated a name behind the scenes anyway), how can we refer to it? The answer is to have the compiler infer the type:

It's clear the type used in the select "projection" clause is used to shape our resulting objects, so it should appear somewhere on the surface of our query. This is illustrated in Figure 7.14. In fact, I'm temporarily driving attention away from the enumeration aspect that comes with a query: Before we can enumerate over elements, the foreach statement requires us to state the type somehow. Here we can't do anything but have the compiler infer it for us:

```
foreach (var memoryHungryProcess in memHungry)
{
    Console.WriteLine(memoryHungryProcess);
}
```

![](bbox=[0.15, 0.8, 0.7, 0.92])

# FIGURE 7.14 The anonymous type used in the select clause propagates to the result.

Figure 7.15 shows the result of running the query by means of iteration using the foreach loop construct. Notice that anonymous types have a ToString override in place that prints their property names and values in a comma-separated string. Handy.