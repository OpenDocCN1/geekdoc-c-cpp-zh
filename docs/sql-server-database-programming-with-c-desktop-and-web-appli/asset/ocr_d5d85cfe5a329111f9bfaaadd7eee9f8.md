faculty faculty = new Faculty();
faculty.faculty_id = "B78880";
faculty.faculty_name = "Ying Bai";
faculty.office = "MTC-211";
faculty.title = "Associate Professor";

**FIGURE 4.66** Example of using the object initializer.

an instance is created. Object initializers allow creating a new instance with all necessary initializations being performed at the same time as the instantiation process.

# 4.9.4 Query Expressions

To perform any kind of LINQ query, such as LINQ to Objects, LINQ to ADO.NET, LINQ to XML, a valid query expression is needed. The query expressions in C# 3.0 have a syntax that is closer to SQL statements and are composed of some clauses. The most popular query expressions are the foreach statement. As this is executed, the compiler converts it into a loop with calls such as GetEnumerator() and MoveNext(). The main advantage of using the foreach loop to perform the query is it provides a significant simplicity in enumerating arrays, collections and returns the results in an easy way. A typical syntax of query expression is shown in Figure 4.67.

Generally, a query expression is composed of two blocks. The top block in Figure 4.67 is the from-clause block and the query-body block is the query-body block. The from-clause block only takes charge of the query information (no query results), but the query-body block performs the real query and contains the real results.

Referring to the syntax represented in Figure 4.67, the following components should be included in a query expression:

+   * A variable must be defined first either explicitly (IEnumerable<T>) or implicitly (var) type.
* A query expression can be represented in either query syntax or method syntax.
* A query expression must start with a from clause and must end with a select or group clause. Between the first from clause and the last select or group clause, it can contain one or more of these optional clauses: where, order by, join, let and even additional from.

In all LINQ queries using LINQ to DataSet, all of the clauses will be converted to the Standard Query Operator methods, such as From(), Where(), OrderBy(), Join(), Let() and Select(), as the

```
var query_variable = in [data source]
let [expression]
where [boolean expression]
order by [[expression](ascending/descending)], [optional repeat]
select [expression]
group [expression] by [expression] into [expression]

foreach (range_variable in query_variable)
{
// pick or retrieve back each element from the range_variable....
}
```

**FIGURE 4.67** A typical syntax of query expression.