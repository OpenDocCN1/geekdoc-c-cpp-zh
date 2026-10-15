
# Index of 3.0 Topics

Operators
=> (equal sign, greater than) lambda operator, 517

## A

- Action delegates, 524-525
- Aggregate functions, 618
- Anonymous functions, 516, 517
- Anonymous methods, internals, 527-528
- Anonymous types
  - definition, 572
  - generating, 578
  - implicit local variables, 572-576
  - in query expressions, 625-626
  - type incompatibilities, 576-577
  - type safety, 576-577
  - var keyword, 572-576
- AsParallel() operator, 595
- Automatically implemented properties
  - description, 240-242
  - internals, 254
- Average() method, 618

## B

- BinaryExpression, 535
- bool, returning in lambda expressions, 520

## C

- C++ vs. C#
  - var keyword, 575
  - Variant, 575
  - void*, 575
- Caching data, 600
- Captured variables, 528-530
- Capturing loop variables, 531-533
- Cartesian products, 608, 638-639
- Chaining multicast delegates, 555
- Class collections, filtering, 591
- Classes, inextensible, 273-275
- Closed over variables, 528-530
- Closures, 531
- Collection initializers
  - definition, 578
  - initializing anonymous type arrays, 581-582
  - initializing collections, 579
- Collections
  - class, filtering, 591
  - discarding duplicate members, 639-640
  - filtering, 622
  - projecting, 622
  - returning distinct members, 639-640
- Collections, sorting
  - by file size, 633-634
  - orderby clause, 632-633
  - with query expressions, 632-633
- Compile() method, 535
- Concat() operator, 618
- Constructors, object initializers, 257-259
- Continuation clauses, query expressions with LINQ, 637-638
- Count() method, 595-596, 618

## D

- DefaultIfEmpty(), 613-614
- Deferred execution
  - description, 597-598
Deferred execution (continued)
  - expression trees, 630-631
  - implementing, 630-631
  - query expressions with LINQ, 627-631
  - unintended triggering of standard query operators, 600-601
- Delegates
  - contravariance, 526-527
  - covariance, 526-527
  - creating with a statement lambda, 517-518
  - deferred execution, 630-631
  - vs. expression trees, 536-537
  - general purpose, 524-525
  - guidelines, 525
  - passing with expression lambdas, 520
  - structural equality, 526-527
  - System.Action, 524-525
  - System.Func, 524-525
- Derivation, extension methods, 299
- DirectoryInfoExtension.Copy() method, 275-277
- Discarding duplicate members, query expressions with LINQ, 639-640
- Distinct() operator, 618, 639-641

## E

- Error handling, multicast delegates, 554-556
- Explicitly declared parameter types, 518
- Expression lambdas, 520
- Expression trees
  - BinaryExpression, 535
  - building LINQ queries, 537-538
  - Compile() method, 535
  - deferred execution, 630-631
  - definition, 533
  - vs. delegates, 536-537
  - examining, 538-541
  - lambda expressions as data, 534-535
  - LoopExpression, 535
  - MethodCallExpression, 535
  - NewExpression, 535
  - as object graphs, 535-536
  - ParameterExpression, 535
  - UnaryExpression, 535
- Extension methods, 275-277, 341-343

## F

- FileInfo collections, projecting, 633-634
- FileInfo object, 593, 625, 633
- Filtering collections
  - class collections, Where() method, 597-598
  - collections, 591, 622, 631-632
  - query expressions with LINQ, 631-632
  - where clause, 631-632
  - Where() method, 591
- Filtering with Where(), 591-592, 597-598
- Flattening a sequence of sequences, query expressions with LINQ, 638-639
- from clause, query expressions with LINQ, 623-624, 638-639
- Full outer join, definition, 604
- Func delegates, 524-525

## G

- GetType() method, 520
- group by clause, query expressions with LINQ, 635-637
- GroupBy() method, grouping results, 610-611
- group clause, query expressions with LINQ, 623
- Grouping query results, 634-637
- GroupJoin() method, 611-613

## I

- IListable interface, 342-343
- Implicitly typed local variables, declaring, 60-61
- In type parameter, 526
- Inner join, 604, 607-610
- Instance methods, adding to a class, 276
- Interfaces, extension methods, 341-343
- Intersect() operator, 618
- into keyword, query expressions with LINQ, 637
- IQueryable<T> interface, custom LINQ providers, 619

## J

- JavaScript vs. C#
  - var keyword, 575
  - Variant, 575
  - void*, 575
- Join() method, 607-610
- Join operations, standard query operators
  - Cartesian products, 608
  - DefaultIfEmpty(), 613-614
  - full outer join, 604
  - grouping results with GroupBy(), 610-611
  - inner join, 604, 607-610
  - introduction, 603-604
  - left outer join, 604
  - many-to-many relationships, 604
  - normalized data, 607-608
  - one-to-many relationships, 604
  - one-to-many relationships, with GroupJoin(), 611-613
  - outer joins, with GroupJoin(), 613-614
  - outer joins, with SelectMany(), 613-616
  - right outer join, 604

## L

- Lambda expressions
  - => (equal sign, greater than) lambda operator, 517
  - captured variables, 528-530
  - capturing loop variables, 531-533
  - closed over variables, 528-530
  - closures, 531
  - as data, 534-535
  - definition, 516
  - explicitly declared parameter types, 518
  - expression lambdas, 520
  - GetType() method, 520
  - guidelines, 518
  - internals, 527-528
  - lifetime of captured variables, 530
  - notes and examples, 521-522
  - outer variable CIL implementation, 530-531
  - outer variables, 528-530
  - predicate, definition, 520, 591
  - returning a bool, 520
  - sequence of operations, 599
  - statement lambdas, 517-519
  - typeof() operator, 520
- Left outer join, definition, 604
- let clause, query expressions with LINQ, 633-634
- Lifetime of captured variables, 530
- Local variables, implicitly typed, 60-61
- Loop variables, capturing, 531-533
- LoopExpression, 535

## M

- Many-to-many relationships, definition, 604
- Max() method, 618
- MethodCallExpression, 535
- Methods, partial, 285-288
- Min() method, 618
- Monads, definition, 591
- Multicast delegates
  - chaining, 555
  - error handling, 554-556

## N

- .NET versions, 29
- NewExpression, 535
- Normalized data, 607-608

## O

- Object initializers
  - calling, 257-259
  - definition, 257
- OfType() operator, 618
- One-to-many relationships, 604, 611-613
- orderby clause, sorting collections, 632-633
- OrderByDescending(), 602
- OrderBy() method, sorting class collections, 601-603
- Outer joins
  - with GroupJoin(), 613-614
  - with SelectMany(), 613-616
- Outer variables, 528-531

## P

- ParameterExpression, 535
- Partial methods, 285-288
- Predicate
  - definition, 520, 591
  - filtering class collections, 591
- Projecting collections
  - definition, 622
  - FileInfo collections, 633-634
  - with query expressions, 624-627
- Properties, automatically implemented
  - description, 240-242
  - internals, 254

## Q

- Query expressions with LINQ
  - code example, 622-623
  - continuation clauses, 637-638
  - deferred execution, 627-631
  - definition, 621
  - discarding duplicate members, 639-640
  - filtering collections, 631-632
  - flattening a sequence of sequences, 638-639
  - from clause, 623-624, 638-639
  - group by clause, 635-637
  - group clause, 623
  - grouping query results, 634-637
  - guidelines, 641
  - into keyword, 637
  - introduction, 622-624
  - let clause, 633-634
  - projecting collections, 624-627
  - range variables, 622-623
  - returning distinct members, 639-640
  - select clause, 623-624
  - sorting collections, 632-633
  - translating to method calls, 640-641
- Query results, grouping, 634-637
- Queryable extensions, 619

## R

- Race conditions, 595
- Range variables, query expressions with LINQ, 622-623
- Returning distinct members, query expressions with LINQ, 639-640
- Reverse() operator, 618
- Right outer join, definition, 604
- Running LINQ queries in parallel, 594-595

## S

- Sample classes, 588-591
- select clause, query expressions with LINQ, 623-624
- Select() method, 592-594, 615-616
- SelectMany() method
  - calling, 614-616
  - creating outer joins, 613-616
  - vs. Select(), 615-616
- Sequence diagram, 599
- SequenceEquals() operator, 618
- Sorting, collections
  - by file size, 633-634
  - orderby clause, 632-633
  - with query expressions, 632-633
- Sorting, standard query operators
  - ascending order ThenBy(), 601-603
  - ascending order with OrderBy(), 601-603
  - descending order with OrderByDescending(), 602
  - descending order with ThenByDescending(), 602
- Standard query operators
  - AsParallel(), 595
  - caching data, 600
  - Concat(), 618
  - counting elements with Count(), 595-596
  - deferred execution, 597-598, 600-601
  - definition, 588
  - Distinct(), 618
  - filtering with Where(), 591-592, 597-598
  - guidelines, 596, 641
  - Intersect(), 618
  - OfType(), 618
  - queryable extensions, 619
  - race conditions, 595
  - Reverse(), 618
  - running LINQ queries in parallel, 594-595
  - sample classes, 588-591
  - sequence diagram, 599
  - SequenceEquals(), 618
  - System.Linq.Enumerable method calls, 616-617
  - table of, 618
  - Union(), 618
- Standard query operators, join operations
  - Cartesian products, 608
  - DefaultIfEmpty(), 613-614
  - full outer join, 604
  - grouping results with GroupBy(), 610-611
  - inner join, 604, 607-610
  - introduction, 603-604
  - left outer join, 604
  - many-to-many relationships, 604
  - normalized data, 607-608
  - one-to-many relationships, 604
  - one-to-many relationships, with GroupJoin(), 611-613
  - outer joins, with GroupJoin(), 613-614
  - outer joins, with SelectMany(), 613-616
  - right outer join, 604
- Standard query operators, sorting
  - ascending order ThenBy(), 601-603
