lot more cumbersome and unobvious when mistakes are made against types, database schemas, or when dealing with complex join operations.

![](bbox=[0.08, 0.2, 0.48, 0.54])

FIGURE 19.2 No compile-time checking of query statements.

However, more problems come from using an opaque string as the input to the server. Because the query command doesn't get verified extensively before being sent to the server, it's susceptible to different types of attacks when the query string gets built improperly. A typical source of errors is in the parameterization of queries:

```
string query = "SELECT * FROM Products WHERE Name='" + name + "'";
```

If the name variable comes from an untrusted source, like the user providing direct input through some UI, several problems can arise with the preceding code. What if the name contains the following?

```
' OR TRUE --
```

This results in a query that has a WHERE clause looking like this:

```
WHERE Name='' OR TRUE --'
```

The -- is SQL's comment syntax, making the remainder of the line invisible to the query execution engine. Clearly, the preceding query will return all results instead. This just shows the tip of the iceberg of query attacks, with much more severe ones possible:
'; DROP DATABASE Northwind --
Oops, if the connection to the database server was made with an account that has the right to drop a database, the user can delete the whole database by putting well-crafted input in the "name" input field. This category of attacks is known as SQL injection attacks.