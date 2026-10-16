What we have is a newly created class called Person. It contains two member variables called age and name. We can use a constructor to initialize the variables. In our Main method, five objects were created of this class and stored in a list collection called plist. Then a LINQ query was executed using both the where and the select operators. We use the where operator to filter the objects with a lower age than 10 – if we omit the select operator, we would see the entire Person object returned. Because we only want the names of those who are younger than 10, the select operator is used. We pass the operator lambda expression which will select the name of the person.

Those are two of the LINQ query operators that you will use the most in your programs. I really could continue, but we don’t have the space or time to discuss every operator – the entire subject of LINQ would take a book of its own – so we’ll move on and look at how to connect LINQ to both SQL and to XML.

What really gives LINQ the edge over other similar technologies is the flexibility it has to work with several data types. What that means is that LINQ uses the same query syntax to handle incoming data independently of the source type for the data, where the other technologies require you to write a different query for each separate source. For example, you would need an SQL query if you wanted to interact with the SQL server and to interact with the XML data type, you would need an XQuery. What we are going to look at here is the relationship between LINQ and SQL, and LINQ and Lambda expressions.

# LINQ and SQL

Using LINQ is the smart choice as an alternative to using the old-fashioned way of SQL queries to access SQL data. Where you see the term LINQ to SQL, it is usually describing a relationship by which we can use LINQ to access the SQL databases. The first thing we need to do is map the target or existing SQL database to LINQ.

# Mapping LINQ to SQL