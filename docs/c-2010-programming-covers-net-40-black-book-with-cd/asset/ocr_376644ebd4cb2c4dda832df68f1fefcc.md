Let’s learn the basics of SQL in the next section.

# The SELECT Statement

You can use the SELECT statement to get fields from a table. The following is an example to retrieve all the records in the Customers table, by using the wildcard character *:

```
SELECT * FROM Customers
```

The preceding example returns a DataSet that holds all the records in the Customers table. You can also use the SELECT statement to select specific fields from a table, as shown in the following example:

```
SELECT CustomerID, Address, City FROM Customers
```

In the preceding example, you can retrieve the CustomerID, Address, and City fields from the Customers table. The preceding example returns a DataSet that holds all the records in the Customers table, and each record has a CustomerID, Address, and City field.

# The WHERE Clause

In SQL, you can use the WHERE clause to specify a criterion that you want all the records to meet. For example, to select all the records in the Customers table, where the City field holds London, you can execute the following statement:

```
SELECT * FROM Customers WHERE City = 'London'
```

The other operators that can be used in the WHERE clauses are as follows:

+   - < (less than)
+   - <= (less than or equal to)
+   - > (greater than)
+   - >= (greater than or equal to)
+   - BETWEEN
+   - IN
+   - LIKE

# The LIKE Clause

In SQL, the LIKE clause allows you to use the partial string that you can specify with wildcards. You can select all the records from the Customers table, where the City field matches the wildcard string Lo%. This is shown in the following SQL query statement:

```
SELECT * FROM Customers WHERE City LIKE 'Lo%'
```

The preceding example creates a DataSet which contains only those records whose City field contains names starting with Lo, such as Los Angeles or London. The three possible combinations for using the % wildcard character are as follows:

+   - Lo% — Returns all the items starting with Lo, such as London or Los Angeles.
+   - %Lo — Returns all the items ending with Lo, such as São Paulo.
+   - %Lo% — Returns all the items containing Lo anywhere in the field value, such as Barcelona.

# The DISTINCT Clause

Sometimes a database may hold duplicate values in the fields of a table. For example, several customers come from the same cities, so they would have the same value in the City field. You might want to take a look at all the cities represented, without repetition. You can use the DISTINCT clause to avoid repetition, as shown in the following SQL query statement:

```
SELECT DISTINCT City FROM Customers
```

# The Logical Operators

The logical operators are used in a situation when you need to retrieve the records from the database on the basis of some logical conditions. Let’s take an example in which you want to retrieve only those records whose city should neither be Boston or York, and the Fax field should have some value (we use the IS NOT NULL