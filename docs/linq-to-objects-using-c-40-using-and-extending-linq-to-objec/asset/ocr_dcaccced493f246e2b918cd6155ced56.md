```
{
  name = fields[nameColumn] ?? "",
  elevation = fields[elevationColumn] ?? "",
  country = fields[countryColumn]
}
.AsSequential()
.Take(5);
```

The indicative performance of each of these queries can be measured as

q = 29.1 seconds (Sequential)
q1 (Listing 9-4) = 30.7 seconds
q2 (Listing 9-5) = 23.3 seconds

This example demonstrates the need to be diligent about understanding what impact some operators have on the ability to add an AsParallel to a query. Developers must be diligent about profiling and measuring query performance when invoking the parallel operators.

# Two-Source Operators and AsParallel

There are a number of operators in LINQ that take two data sources:

+   - Concat
- Except
- GroupJoin
- Intersect
- Join
- SequenceEqual
- Union
- Zip

When parallelizing queries that use any of these binary operators, both data sources must be marked with the AsParallel operator (and optionally withOrdered) to avoid a runtime exception being raised. Early versions of the Parallel LINQ extensions didn't enforce this dual opt-in process, and it was difficult to specifically control the ordering semantics of those queries. Forcing the developer to explicitly control the ordering semantics bridges this gap and makes queries predictable.

Failing to specify the second data source as parallel causes an obsolete warning during compilation with instructions on how to resolve the issue.