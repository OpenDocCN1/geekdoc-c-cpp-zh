# Mapping Entity Type to Multiple Tables

A fairly common problem in database applications is the mismatch between the shape of database tables and entity types. For example, a common database optimization technique is to separate frequently accessed columns from rarely accessed ones by placing them in two separate tables. The idea is to reduce the amount of data that has to be read from disk during table or index scan operations. This scenario can be illustrated by splitting the Customers table from the Northwind database in two—Customer and CustomerAddress:

```
```sql
create table split.Customer(
    CustomerID nchar(5) not null primary key,
    CompanyName varchar(40),
    ContactName nvarchar(30) not null,
    ContactTitle nvarchar(30)
);
```
```

```
```sql
create table split.CustomerAddress(
    CustomerID nchar(5) not null primary key,
    Address nvarchar(60),
    City nvarchar(15),
    Region nvarchar(15),
    PostalCode nvarchar(10),
    Country nvarchar(15),
    Phone nvarchar(24),
    Fax nvarchar(24)
);
```
```

Even though the Customer information is now split in two tables, definition of the Customer entity in the conceptual model does not have to change—it continues to have both contact and address properties. You can map it to two tables instead of one; Figure 2.12 shows how this looks in the Mapping Details window of the Entity Designer. When the entity mapping has been modified, you can continue working with it in the application code as if it were still mapped to a single table:

```
```csharp
var query = from c in context.Customers
            select c;
foreach (Customer c in query)
    Console.WriteLine(c.ContactName + " " + c.Address);
```
```

Under the hood, the Entity Framework automatically generates the SQL join queries required to retrieve the customer information from what is now two tables, allowing you to keep a holistic view of the Customer entity in the application code.