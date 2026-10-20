# Basic concepts for working with LINQ

As its name implies, LINQ, or Language-Integrated Query, lets you query a data source using the C# language. Before you learn how to code LINQ queries, you need to learn some concepts related to LINQ, such as how LINQ is implemented and what the three stages of a query operation are. In addition, you’ll want to know the advantages you’ll get from using LINQ.

# How LINQ is implemented

LINQ is implemented as a set of methods that are defined by the Enumerable and Queryable classes. Because these methods can only be used in a query operation, they’re referred to as query operators. Although you can call the query operators directly by coding a method-based query, you can also use the clauses C# provides that give you access to the operators. When you use C# clauses to code a LINQ query, the result is called a query expression.

Figure 18-1 presents the C# clauses you’re most likely to use in a query expression. If you’ve ever coded a query using SQL, you shouldn’t have any trouble understanding what each of these clauses does. For example, you use the from clause to identify the data source for the query. You use the where clause to filter the data that’s returned by the query. And you use the select clause to identify the fields you want to be returned by the query. You’ll learn how to code queries that use all of these clauses later in this chapter.

# Advantages of using LINQ

Figure 18-1 also lists several advantages of LINQ. Probably the biggest advantage is that it lets you query different types of data sources using the same language. As you’ll see in this chapter, for example, you can use the same language to query an array and a generic list of objects. Keep in mind as you read this chapter, though, that you can use these same skills to query more sophisticated data sources such as databases and entity objects defined by Entity Framework.

The key to making this work is that the query language is integrated into C#. Because of that, you don’t have to learn a different query language for each type of data source. In addition, as you enter your queries, you can take advantage of the IntelliSense features that are provided for the C# language. The compiler can catch errors in the query, such as a field that doesn’t exist in the data source, so you don’t get errors at runtime. And when a runtime error does occur, you can use the Visual Studio debugging features to determine its cause.

Finally, if you’re working with a relational data source such as a SQL Server database, you can use an object-relational mapper (ORM) like Entity Framework to develop an object-relational mapping. Then, you can use LINQ to query the objects defined by this mapping, and the query will be converted to the form required by the data source. This can make it significantly easier to work with relational data sources.