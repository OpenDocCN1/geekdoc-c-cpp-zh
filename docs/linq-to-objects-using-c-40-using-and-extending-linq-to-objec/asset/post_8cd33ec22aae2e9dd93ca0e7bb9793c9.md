
# Output 4-7

Customer: Barney Gottshall
Year: 2006
Month: August
8/7/2006 8:12:00 AM - for 2 minutes
8/7/2006 1:12:00 PM - for 15 minutes
8/7/2006 1:47:00 PM - for 3 minutes
Month: July
7/12/2006 8:12:00 AM - for 5 minutes
7/7/2006 1:47:00 PM - for 21 minutes
Month: June
6/7/2006 1:12:00 PM - for 10 minutes

Customer: Armando Valdes
Year: 2006
Month: August
8/8/2006 2:00:00 PM - for 3 minutes
8/8/2006 2:37:00 PM - for 7 minutes
Month: July
7/8/2006 2:00:00 PM - for 32 minutes
7/8/2006 2:37:00 PM - for 13 minutes

Customer: Ariel Hazelgrove
Year: 2006
Month: August
8/7/2006 9:23:00 AM - for 15 minutes
Month: June
6/14/2006 9:23:00 AM - for 12 minutes

# How to Join with Data in Another Sequence

The basis of any Relational Database Management System (DBMS) is the ability to draw together data from multiple sources (tables generally) as the result of a query; this is called “Joining” data. In relational databases, the joins are most often between primary key and foreign key-related columns, but a join can be achieved on any data as long as both data sources share a common column value. One fundamental reason for splitting data into multiple sources is to avoid duplicating data—this process is called normalization by database developers.

Although the concept of joining-in-memory collections isn't a common pattern today (it's more likely that you nest a collection inside another object to indicate a parent-child relationship). LINQ to Objects introduces the concept of joining multiple data sources through its powerful Join and GroupJoin operators and their equivalent query expression syntax options. LINQ also enables join-clause by using a subquery expression within the Select clause. This subquery of coding is often simpler to read and helps you avoid having to use any specific Join syntax in the query at all. Both techniques are covered in the examples throughout this chapter.

There are three basic styles of Joins that are commonly used when drawing data from multiple sources based on a shared key value:

- **Cross Join**—Every element in the first sequence (the outer) is projected with every element in the second sequence (the inner), often called the Cartesian Product. An example for this type of join is when you want to systematically access each pixel in a bitmap by its x and y locations.
- **One-to-One Inner Join**—This type of join allows you to access data in both sequences based on a common column value. The resulting sequence is flat (there is no subgroup). An example use for type of join is when you want to access data from another sequence to extend the data you have on some element.
- **One-to-Many Join**—This type of join allows you to use the first sequence record as a key for a subgroup sequence where a given column value is used as the referential key. An example of this type of join is having a list of orders for a set of given customers.

There are numerous ways in LINQ to achieve each of these join types. Each technique and its relative merit is discussed next.

# Cross Joins

Cross joins project every element in one sequence against every element in a second sequence. Cross joins in LINQ to Objects ironically aren't implemented using either of the Join operators, but rather a clever use of the SelectMany operator. The query expression syntax will be familiar (not identical) to anyone with knowledge of standard SQL joins. In LINQ query expression syntax, you simply specify multiple from statements, as shown in the following code:

```
var outer = Enumerable.Range(1, 3);
var inner = Enumerable.Range(1, 3);
```

```
var q = from x in outer
   from y in inner
   select new { x, y };
```

```
foreach (var element in q)
   Console.WriteLine("{0}, {1}", element.x, element.y);
```

The result from this query will be the Cartesian Product, which is a fancy term for all values in the outer range, x (with values 1, 2, and 3) against each value in the inner range, y (with values 1, 2, and 3) as shown in the following result:

- 1, 1
1, 2
1, 3
2, 1
2, 2
2, 3
3, 1
3, 2
3, 3

The following code, which is identical to the previous query except that it is written in extension method syntax, shows how the query expression syntax (using multiple from statements) is mapped to the SelectMany operator. The result that yields is identical as well:

```
var q1 = outer
   .SelectMany(
      inner,
      (x, y) => new { x, y }
   );
```
