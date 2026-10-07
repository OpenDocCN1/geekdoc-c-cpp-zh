# Introduction to Language Integrated Query (LINQ)

```
string[] fruits = { "apple", "banana", "mango", "orange", "blueberry", "grape", "strawberry" };
List<int> lengths = fruits.Select(fruit => fruit.Length).ToList();
foreach (int length in lengths)
    Console.WriteLine(length);
```

// the running result of this piece of codes is:

+   5
6
6
9
5
10

**FIGURE 4.17** A piece of codes for the operator ToList.

provide an introduction about the LINQ query. Then we divide this discussion into seven sections:

+   1. Architecture and Components of LINQ
2. LINQ to Objects
3. LINQ to DataSet
4. LINQ to SQL
5. LINQ to Entities
6. LINQ to XML
7. C# 3.0 Language Enhancement for LINQ

Three components, LINQ to DataSet, LINQ to SQL, and LINQ to Entities, belong to LINQ to AD.NET. Now let's start with the first part, introduction to LINQ query.

# 4.2 INTRODUCTION TO LINQ QUERY

A query is basically an expression that retrieves data from a data source. Queries are usually expressed in a specialized language such as Microsoft Access, SQL Server, Oracle or XML document. Languages have been developed over time for the various types of data sources, for example SQL for relational databases and XQuery for XML. Developers have to learn a new query for each type of data source or format that they must support. LINQ simplifies this situation by using a consistent model for working with data across various kinds of data sources and formats. In LINQ query, you are working with objects. You use the same basic coding patterns to query and transform data in XML documents, SQL databases, AD.NET collections, and any other format for which a LINQ provider is available.

LINQ can be considered as a pattern or model that is supported by a collection-called Standard Query methods, and all those Standard Query methods are static methods defined in either IEnumerable or IQueryable classes in the namespace System.Linq. The data operated in LINQ query are sequence objects with the type of either IEnumerable<T> or IQueryable<T>, where T is the actual type of data stored in the sequence.

From another point of view, LINQ can also be a converter or bridge that sets up a mapping relationship between the abstract objects implemented in Standard Query operators and the physical reality implemented in the real world. It is LINQ that allows developers to directly access and manipulate data in different databases using the same basic coding patterns. With the help of LINQ, the difficulty caused by learning and using different syntaxes, formats and query structures for different data sources in order to access and query them can be