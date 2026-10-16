+   - Queries with a Skip, SkipWhile, Take or TakeWhile operator and where the source sequence indices are no longer in their original order
+   - Queries with SequenceEquals or Zip, with the exception of any data source whose index is in the original order and the other data source is an IList(T), array, or another one that can be indexed
+   - Queries with Concat unless it has been applied to a data source that can be indexed
+   - Queries with Reverse, unless it has been applied to a data source that can be indexed

# PLINQ Order Preservation

You already know that PLINQ has one main goal – maximum performance while keeping everything correct. Queries should be able to run as fast as they possibly can while producing the right results. Sometimes, the requirement for correct results will require preservation of the source sequence order, but ordering can come at a high computational cost. Therefore, PLINQ, by default, will not preserve that order. In this sense, it is much like a LINQ to SQL query but not like the LINQ to Objects query, where order preservation is required.

You can, however, override the default and enable order preservation and you do that by using the operator called AsOrdered on the source sequence. Then, order preservation can be disabled later with the operator called AsUnordered. On both of these, the query processing will be based on whatever heuristic determines whether parallel or sequential execution should be done.

In the next example, you can see a parallel query, unordered, and filtering for any element that matches a specific condition without attempting to order the results.