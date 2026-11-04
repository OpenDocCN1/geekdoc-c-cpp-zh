In Fig.C#10.2, you can see that on clicking the Click button, the listView1 list view displays the numbers that are divisible by 2.

Now, let's discuss the standard query operators available in LINQ in the following sections.

# Exploring Standard Query Operators

The standard query operators are clauses that are used to create and refine data based on a query and the needs of an application. Standard query operators can be thought of as methods that can be used to perform querying on any .NET array or collection. Some of the standard query operators include filtering, projection, partitioning, grouping, aggregation, and sorting. The standard query operators in LINQ are an Application Programming Interface (API) that enables querying of any .NET array, collection, or a sequence of data.

The various standard query operators available in LINQ differ from each other in the time they take to execute the query. The time depends on whether they have to return a single value or a sequence of values. The methods that return a single value execute immediately, while the methods that return a sequence of values reschedule the execution of the query before returning an output.

Table 10.1 lists the standard query operators used in LINQ:

Table 10.1: Standard Query Operators in LINQ

| Operator Type | Description |
|---|---|
| Sorting operator | Changes the order of the elements of a sequence returned by a query |
| Set operator | Returns a result set in the form of a collection |
| Filtering operator | Restricts a result set to contain those elements that satisfy a specific condition |
| Quantifier operator | Returns a Boolean value, which is either True or False |
| Projection operator | Transforms an object into a new object |
| Partitioning operator | Divides the input sequence into two sections and returns one section |
| Join operator | Combines collections |
| Grouping operator | Arranges data into groups |
| Generation operator | Creates a new sequence of values |
| Element operator | Returns a single, specific element from a collection |
| Conversion operator | Converts a collection to an array |
| Aggregate operator | Computes a single value from a collection |
| Equality operator | Checks whether two sequences are equal or not |
| Concatenation operator | Appends one sequence of elements to another |

Now, let's discuss the preceding standard query operators one by one in detail, in the following sections.

# The Sorting Operators

The sorting operators in LINQ order the elements of a sequence based on one or more attributes. You can sort the elements of a sequence with one specific attribute and perform primary sorting on the elements. You can then specify the second sorting criterion and sort the elements within the primary sorted group. The important sorting operators in LINQ are the orderby and orderbydescending clauses.

The sorting functionality is achieved by using the orderby clause. A sorting operator can sort data in either ascending or descending order. The default behavior of the orderby clause is to sort data in ascending order. If you want to sort data in descending order, you need to use the orderbydescending clause.

Now, let's create a Windows application called SortingOperator, where you can use the orderby and orderbydescending clauses to sort data. For this, perform the following steps: