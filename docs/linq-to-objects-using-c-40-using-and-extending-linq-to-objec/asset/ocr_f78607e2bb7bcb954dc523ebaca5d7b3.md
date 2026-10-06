# Table 1-1 Standard Query Operators in the .NET Framework 4 Release

| Operator Type | Standard Query Operator Name |
|---|---|n| Equality | SequenceEqual |
| Generation | Empty, Range, Repeat |
| Grouping | GroupBy, ToLookup |
| Joining | GroupJoin, Join |
| Merging | Zip |
| Ordering | OrderBy, ThenBy, OrderByDescending, ThenByDescending, Reverse |
| Projection | Select, SelectMany |
| Partitioning | Skip, SkipWhile, Take, TakeWhile |
| Quantifiers | All, Any, Contains |
| Restriction | Distinct, Where |
| Set | Concat, Except, Intersect, Union |

Many of the standard Query operators are identical to those found in database query languages, which makes sense; if you were going to design what features a query language should have, looking at the current implementations that have been refined over 30 years is a good starting point. However, some of the operators introduce new approaches to working with data, simplifying what would have been complex traditional code into a single statement.

# Open and Extensible Architecture

LINQ has been designed with extensibility in mind. Not only can new operators be added when a need arises, but entire new data sources can be added to the LINQ framework (cave: operator implementation often needs to consider data source, and this can be complex—point is that it's possible, and for LINQ to Objects, actually pretty simple).

Not only are the LINQ extension points exposed, Microsoft has implemented their specific providers using these extension points. This will ensure that any provider, whether it be from open-source community projects to competitive data-access platforms, will compete on a level playing field.