Now, when you're using LINQ to SQL or other IQueryable<T>-based LINQ providers, think of the nice interaction between compile-time expression tree generation and the Queryable extension methods role in stitching those fragments together to provide a wholesale query expression to the query provider underneath. A whole set of query providers exist, many of which leverage this technique:

+   - LINQ to SQL, LINQ to Entities (in .NET 3.5 and later)
+   - LINQ to SharePoint (starting with Office 2010)
+   - LINQ to Amazon (the first IQueryable<T> provider I am aware of)
+   - LINQ to... Anything?

# Summary

To understand how LINQ to Objects works for in-memory queries over collections, a solid knowledge of C# 2.0 iterators is required. After introducing this language feature, we put it into practice by implementing a few iterators that behave like query operators. One key takeaway from the way iterators work is the concept of lazy evaluation.

Following the intermezzo on iterators, we explored the rich set of query operators in more depth, examining the behavior of those operators. Collectively known as the standard query operators, they form the heart of LINQ queries. Query expression syntax provided by languages such as C# turns into calls to those operator methods.

Because one of the things that LINQ allows is the capability to put the runtime in control over the way queries execute, we illustrated this powerful concept in a brief detour through .NET 4's Parallel LINQ implementation. The declarative nature of LINQ not only results in more readable code, it also permits future optimizations carried out by framework writers.

Finally, because one the goals of embedded querying capabilities is to span multiple data domains, we studied the mechanics that allow queries to be translated into specialized query languages at runtime. Starting with the essentials of expression trees, we ended up in the world of IQueryable<T>, where query providers get to see a query expression in its entirety, ready for customized handling at runtime.