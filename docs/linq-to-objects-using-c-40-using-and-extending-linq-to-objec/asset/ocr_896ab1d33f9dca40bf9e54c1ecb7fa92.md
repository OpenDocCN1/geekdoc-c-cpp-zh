# 284 CHAPTER 9 PARALLEL LINQ TO OBJECTS

Table 9-1 Query Execution Times for the Queries Shown in Listing 9-3

| Query | Execution Time (100,000 loops, single dual-core processor) | Output |
|--- |--- |--- |
| Sequential (q) | 11,047ms | 0 1 2 3 4 5 6 7 8 9 10 |
| Parallel .AsParallel() (q1) | 6,069ms | 6 7 8 9-10 0 1 2 3 4 5 |
| Parallel with orderby (q2) | 6,084ms (This difference is brought about by the data already being ordered and it being such a small set. The OrderBy extension method is expensive on large data sets and should be avoided where possible for performance-sensitive problems.) | 0 1 2 3 4 5 6 7 8 9 10 |
| Parallel .AsOrdered(q3) | 6,036ms (This result is counterintuitive because of the fake MySlowFunction and simplistic example. Forcing order will impact performance on larger data sets and complex queries.) | 0 1 2 3 4 5 6 7 8 9 10 |

The parallel queries did operate faster, as expected. In this case, on a dual-core process, the results were generally slightly less than double. There is overhead in parallelizing, and a key advantage of this code is that with nothing more than the addition of an AsParallel extension to the sequential query, it would likely run close to (but slightly less than) four times faster on a quad-core and eight times on an eight-core processor, and so on, depending on how loaded the CPU is at runtime.