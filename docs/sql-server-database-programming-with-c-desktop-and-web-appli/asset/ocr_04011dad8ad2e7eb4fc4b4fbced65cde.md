# Introduction to Language Integrated Query (LINQ)

After a DataSet has been populated with data, you can begin querying. Formulating queries with LINQ to DataSet is similar to using Language-Integrated Query (LINQ) against other LINQ-enabled data sources. Remember, when you use LINQ queries over a DataSet enumeration of DataRow objects, instead of an enumeration of a custom type. This means that you can query of the members of the DataRow class in your LINQ queries. This lets you create rich and complex queries.

As with other implementations of LINQ, you can create LINQ to DataSet queries in two different forms: query syntax and method-based syntax. Basically, the query syntax will be finally converted to the method-based syntax as the compiling time if the query is written as a query expression, and the query will be executed by calling the Standard Query Operator as the project runs.

# 4.5.1.1 Expression Syntax

A query expression is expressed in query syntax. A query expression is a first-class language construct. It is like any other expression and can be used in any context in a C# expression. A query expression consists of a set of clauses in a declarative syntax to SQL or Query. Each clause contains in one or more C# expressions, and these expressions may themselves be either query expression or contain a query expression.

A query expression must begin with a from clause and must end with a select or group clause. Between the first clause and the last select or group clause, it can contain one or more of these optional clauses: where, order by, let and even from clauses. You can also use the into keyword to enable the result of a join or group clause to serve as the source for additional queries in the query expression.

In all LINQ queries (including LINQ to DataSet), all clauses will be converted to the associated Standard Query Operator methods, such as From. Where. OrderBy. Join, Let and Select, and the queries are compiled. Refer to Figure 4.4 in this Chapter to get the most often used Standard Query Operators and their definitions.

In LINQ, a query is always strongly typed and it can be any variable that stores a query instead of the results of a query. More specifically, a query variable is always an enumerable that will produce a sequence of elements when it is iterated over in a foreach loop or a direct call to its method Enumerator.Next().

The coding example shown in Figure 4.32 illustrates a simple query with one data source, one filtering clause, one ordering clause, and no transformation of the source elements. The select clause ends the query.

An integer is created here and this array works as a data source. The variable scoreQuery is a query and contains only the query command and does not contain any query result. The query is composed of clauses: from, where, order by and select. Both the first and the last clause are returned; the others testScore is typed to int> by using an IEnumerable<T> interface. It is an iteration variable that is scanned through the foreach loop to get and display each queried data when this query is executed. Exactly, when the forecast executes, the queries are not returned through the query variable scoreQuery. Rather, they are returned through the variable testScore.

An alternative way to write this query expression is to use the so-called implicit typing of query variables. The difference between the explicit and implicit typing of query variables is that in the future situation, the relationship between the query variable scoreQuery and the select clause is clearly indicated by the IEnumerable<T> interface, and this makes sure that the type of returned collection is IEnumerable<T> that can be queried by LINQ. In the latter situation, we do not exactly know the data type of the query variable and therefore an implicit type var is used to instruct the compiler to infer the type of a query variable (or any other local variable) at the compiling time.