
## Classes of Object Services

The concept of Object Services is implemented by classes in the System.Data.Objects and System.Data.Objects.DataClasses namespaces. Some classes that are used with Object Services are as follows:

The ObjectContext Class – Represents a primary class for interacting with data in the form of objects that are instances of the entity types defined in EDM. The ObjectContext class encapsulates a connection between .NET Framework and the database. This class serves as a gateway for the CREATE, UPDATE, and DELETE operations. An instance of the ObjectContext class encapsulates the following:

- An EntityConnection object, which specifies a connection to the database
- A MetadataWorkspace object, which describes the model
- An ObjectStateManager object, which manages objects present in the cache

The ObjectContext class uses the System.Data.Objects namespace and System.Data.Entity assembly (in system.data.entity.dll) for working with entity data as objects. The inheritance hierarchy of the System.Data.Objects.ObjectContext class is as follows:

```
System.Object
System.Data.Objects.ObjectContext
```

The syntax to declare the ObjectContext class is as follows:

```
public class ObjectContext : IDisposable
```

The EntityConnection class – Represents a connection to an underlying data store. This class cannot be inherited. You need to use the System.Data.EntityClient namespace and the System.Data.Entity assembly (in system.data.entity.dll) to use this class. The inheritance hierarchy of the System.Data.EntityClient.EntityConnection class is as follows:

```
System.Object
System.MarshalByRefObject
System.ComponentModel.Component
System.Data.Common.DbConnection
System.Data.EntityClient.EntityConnection
```

The syntax to declare the EntityConnection class is as follows:

```
public sealed class EntityConnection : DbConnection
```

The MetadataWorkspace class – Represents the ADO.NET metadata runtime service component that provides support for retrieving metadata from various sources. You need to use the System.Data.Metadata.Edm namespace and the System.Data.Entity assembly (in system.data.entity.dll) to use this class. The inheritance hierarchy of the System.Data.Metadata.Edm.MetadataWorkspace class is as follows:

```
System.Object
System.Data.Metadata.Edm.MetadataWorkspace
```

## Features of Object Services

Object Services provides the following features for programming in Entity Framework:

- **Querying data as objects** – Allows you to use LINQ, Entity SQL, or query builder methods to execute queries for EDM and returns data as objects. Entity Framework contains the ObjectQuery generic class. It represents a query that returns a collection of zero or more typed entities. It is always related to the existing object context that provides the connection and metadata information.
- **Shaping query results** – Returns only those objects that are specifically requested in the query. We can specify whether or not a query returns related objects in case a relationship exists between the objects.
- **Adding, changing, and deleting objects** – Holds data objects in memory and enables us to add, modify and delete objects within an object context.
- **Saving changes to the persisted data store** – Caches changes to objects in the object context. When we call a service explicitly, the changes are stored back to the data store.
- **Binding objects to controls** – Enables binding of objects to controls. These controls must support data bindings such as the DataGridView control.
- **Managing concurrency** – Tracks concurrency when the ConcurrencyMode attribute for one or more properties is set to fixed. Object Services raise specific exceptions when concurrency violations are detected in the application.
- **Attaching and detaching objects** – Refers to the fact that the ObjectContext instance should persist for the duration of application execution. For example, as long as the application executes, the objects should remain bound to Form controls. Objects can be detached to release the resources that are no longer required. It helps in increasing the context size of the object.
- **Serializing objects** – Supports both XML serialization and binary serialization. XML serialization serializes only the public fields and property values of an object into an XML stream, and binary serialization especially proves useful while using ViewState property to persist objects in an ASP.NET application.
- **Managing object identities and tracking changes** – Uses identity values that help to track changes of objects, handle conflicts, and decide when to retrieve data from the data store.
- **Managing connections** – Provide our own connection for the object context, and we can also explicitly manage the connection used by an object.
- **Managing transactions** – Supports .NET Framework transactions to coordinate operations against the data store and enlist distributed transactions. It also supports automatic enlisting of transactions.
- **Using custom objects with an EDM** – Enables you to manually define your own objects or use existing objects with an EDM.

Let’s now learn about Entity SQL language in the next section.

## Understanding Entity SQL Language

Entity SQL is a language similar to SQL, and is provided by ADO.NET Entity Framework to support EDM. Entity SQL supports EDM constructs that enable users to query the data represented by an entity model. Object Services and the EntityClient provider help return data, including scalar results, result sets, and object graphs. Both Object Services and the EntityClient provider enable us to use Entity SQL to execute queries against an EDM and return data as strongly typed CLR objects that are instances of entity types. To create EntityCommand objects, we can specify a stored procedure name or the text of a query by assigning an Entity SQL query string to its System.Data.EntityClient.EntityCommand.CommandText property. Now, let’s discuss the features of Entity SQL in detail.

## Features of Entity SQL

Due to the increasing popularity of e-commerce websites, business applications need to be more interactive while dealing with databases. The use of Entity SQL, provided by ADO.NET Entity Framework, solves many problems of developers in this context, such as performance and ease of handling databases. Some of the features of Entity SQL are as follows:

Inheritance and relationships support—Specifies that the OfType operator in Entity SQL provides the capability of selecting instances of a subtype from a collection of supertype instances. Entity SQL supports EDM features such as inheritance and relationships.

Uniform treatment of subqueries—Specifies that in traditional SQL, a subquery in the FROM clause is considered to be a multiset, but the same subquery used in the SELECT clause is considered to be a scalar subquery. A subquery used on the left-hand side of an IN operator is considered to be a scalar subquery, while that used on the right-hand side is expected to be a multiset subquery. Entity SQL considers all the subqueries to be multiset subqueries and provides the anyelement operator that operates on a collection, such as arrays.

Left correlation and aliasing—Specifies that the Entity SQL generalizes left correlations in the FROM clause and treats them uniformly. In Entity SQL expressions using the FROM clause, we can refer to definitions in the same clause without the need for additional syntax. Entity SQL also imposes additional restrictions on queries involving group by clauses. We can use the following code in Transact-SQL, but it is invalid in Entity SQL:

```
select z.a + z.b from Z as z group by z.a + z.b
```

To perform the same query through Entity SQL, the following syntax is used:

```
select k from Z as z group by (z.a + z.b) as k
```

Expressions contained in the SELECT clause and HAVING clause of such queries may only refer to GROUP BY keys through aliases.

Referencing columns of tables—Specifies that in Entity SQL, all column references must be qualified with the table alias. The following syntax is valid in Transact-SQL, but invalid in Entity-SQL:

```
select x from Z
```

In the preceding expression, we have assumed that x is a valid column of table Z.

The syntax to write the same query by using Entity SQL is as follows:

```
select Z.x as X from Z as z
```

Table aliases are optional in the FROM clause. The name of the table can be used as the implicit alias. The unqualified references in a query can cause certain errors; so, care should be taken during schema evolution.

Support for Expressions—Specifies that for better support of collections and nested collections, Entity SQL treats each line of code as an expression. The following syntax is valid in Transact-SQL, but invalid in Entity-SQL:

```
sal > all (select salary from employees)
sal > any (select salary from employees)
```

Equivalent expressions can be written in Entity SQL as follows:

```
not exists(select 0 from employees as emp where salary > e.salaries)
exists(select 0 from employees as emp where salary > e.salaries)
```

The following are the valid Entity SQL queries:

```
1+2 *3
"abc"
row(1 as a, 2 as b)
{ 1, 3, 5 }
e1 union all e2
set(e1)
```

Navigation through objects—Specifies that Entity SQL uses a specific notation to support navigation through properties of an object. Suppose if emp is an expression of type employee, then the following is the Entity SQL syntax to refer to the address of the city in a table named as employee.

```
emp.Address.City
```

Collection-based aggregates—Specifies that Entity SQL supports two kinds of aggregates, namely, SQL-style aggregates and collection-based aggregates. The syntax of the SQL-style aggregates is as follows:

```
select x, sum(z.y) from Z as z group by z.x as x
```
