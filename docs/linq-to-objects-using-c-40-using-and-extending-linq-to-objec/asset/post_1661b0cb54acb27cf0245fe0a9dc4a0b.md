
## 284 CHAPTER 9 PARALLEL LINQ TO OBJECTS

Table 9-1 Query Execution Times for the Queries Shown in Listing 9-3

| Query | Execution Time (100,000 loops, single dual-core processor) | Output |
| :--- | :--- | :--- |
| Sequential (q) | 11,047ms | 0 1 2 3 4 5 6 7 8 9 10 |
| Parallel .AsParallel() (q1) | 6,069ms | 6 7 8 9-10 0 1 2 3 4 5 |
| Parallel with orderby (q2) | 6,084ms (This difference is brought about by the data already being ordered... small set.) | 0 1 2 3 4 5 6 7 8 9 10 |
| Parallel .AsOrdered(q3) | 6,036ms (This result is counterintuitive because of the fake MySlowFunction... complex example.) | 0 1 2 3 4 5 6 7 8 9 10 |

The parallel queries did operate faster, as expected. In this case, on a dual-core process, the results were generally slightly less than double. There is overhead in parallelizing, and a key advantage of this code is that with nothing more than the addition of an AsParallel extension to the sequential query, it would likely run close to (but slightly less than) four times faster on a quad-core and eight times on an eight-core processor, and so on, depending on how loaded the CPU is at runtime.

## The AsParallel and AsSequential Operators

The AsParallel operator attached to the source of a LINQ query turns a sequential query into a parallel query. (Parallel means the overload operator extending ParallelQuery<T> is called rather than the overload extending IEnumerable<T>.) The AsSequential operator on the other hand, returns the query from that point forward calling the sequential operators (IEnumerable<T> overload rather than Simply, these extension methods allow you to opt-in and opt-out of using the Parallel LINQ extensions from within a query expression.

To maximize the efficiency of LINQ queries, it is sometimes necessary for the developer to take control over what parts of a query are parallel and which parts aren't. Some operators exclude the query from seeing any parallel performance improvement, and in order to allow Parallel LINQ to operate on other parts of a query, some developer intervention is required.

## When to Use the AsSequential Operator

The ability to control what parts of a query are sequential and what parts executed parallel allows you to isolate parts of a query that run slower when executing concurrently. This is often the case when queries are composed (one query as the source of another). When composing queries in this way, it can be useful to force one part to be sequential while another is parallel. A good strategy is carefully consider which parts of a query benefit from parallelization, by inserting it after portion of any query at the end by an AsSequential operator.

Remembering back to the early sections of this chapter where the Parallel LINQ process was described, the initial step in an analysis of the LINQ query is to determine if parallelization is a good fit. This process entails looking at the operators called in a query, and if certain operators are called (particularly on non-indexed collection types), then those queries are executed sequentially. You can use the AsSequential operator to isolate those operators and achieve a greater use of parallelization in the areas that benefit.

The exact rules about when Parallel LINQ will decide to execute a query as sequential (even though you think it AsParallel) is likely to change as Microsoft adds more capabilities into their analysis and operators in the future. At the time of writing, the easiest way to see this occur is to use the Take operator on an IEnumerable<T> (in our case, the anonymous projected result from a query). The following query would execute if source was an unindexed collection:

```cs
var q = source.AsParallel().Take(5);
```

## 286 CHAPTER 9 PARALLEL LINQ TO OBJECTS

To demonstrate this phenomenon, consider the following query, which should run parallel given it has an AsParallel extension. However, Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially.

To demonstrate this phenomenon, consider the following query, which should run parallel given it has an AsParallel extension. However, Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially.

## 288 CHAPTER 9 PARALLEL LINQ TO OBJECTS

Wait, Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially. Listing 9-4 shows a query that due to the AsSequential operator, will run sequentially.

## Two-Source Operators and AsParallel

There are a number of operators in LINQ that take two sources:

- Concat
- Except
- GroupJoin
- Intersect
- Join
- Union
- Zip

When parallelizing queries that use any of these operators, both data sources must be marked with AsParallel (and optionally AsOrdered) to avoid a runtime exception. Early versions of Parallel LINQ didn't enforce this, and it was difficult to specifically control the ordering semantics.
