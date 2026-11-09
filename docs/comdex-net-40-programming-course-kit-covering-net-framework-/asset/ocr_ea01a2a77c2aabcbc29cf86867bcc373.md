# The WHERE Clause

In SQL, you can use the WHERE clause to specify a criteria to retrieve the records. For example, to retrieve all the records from the Customers table, where the value of City field is London, you can use the WHERE clause, as shown in the following SQL statement:

```
SELECT * FROM Customers WHERE City = 'London'
```

As shown in the preceding SQL statement, we have used the = (equal to) operator to specify a criteria in the WHERE clause. In addition to the = operator, you can use the following operators in the WHERE clause:

+   - < (less than)
+   - <= (less than or equal to)
+   - > (greater than)
+   - >= (greater than or equal to)
+   - BETWEEN
+   - IN
+   - LIKE

The comparison operators, such as < and >, are used in the same way as the = operator. Now, let’s see how to use the BETWEEN, IN, and LIKE operators.

# The BETWEEN Operator

You can use the BETWEEN operator to access values that lie in a specified range. For example, if you want to select all the records from the Customers table, where the first letter of the CustomerID field is between R and T (which includes the letters R, S, and T), you can use the BETWEEN operator, as shown in the following SQL statement:

```
SELECT * FROM Customers WHERE CustomerID BETWEEN 'R' AND 'T'
```

# The IN Operator

In SQL, you can use the IN operator to match the values for a given field of a table with a set of specified values. For example, to select those records for which the City field has a value London, Sao Paulo, or Madrid, you can use the IN operator, as shown in the following SQL statement:

```
SELECT * FROM Customers WHERE City IN ('London', 'Sao Paulo', 'Madrid')
```

# The LIKE Operator

The LIKE operator is used to match the values of a field in a table with some specified pattern. You can use the wildcard character % to specify the pattern. For example, to select all the records from the Customers table, where the City field matches the wildcard string Lo%, you can use the LIKE operator, as shown in the following SQL statement:

```
SELECT * FROM Customers WHERE City LIKE 'Lo%'
```

The preceding SQL statement selects all the records for which the City field contains names that match with the pattern Lo%, such as London. The three possible combinations of using the wildcard character % are as follows:

+   - Lo%: Matches the values starting with Lo, such as London or Los Angeles
+   - %Lo: Matches the values ending with Lo, such as São Paulo
+   - %Lo%: Matches the values containing Lo, such as Barcelona

# The DISTINCT Clause

Sometimes, a database has duplicate values in the fields of a table. In such situation, you can use the DISTINCT clause to select values without duplication. For example, several customers may belong to the same city, so the table will have the same value in the City field for those customers. In such a scenario, to retrieve the list of all the cities without duplication, you can use the DISTINCT clause, as shown in the following SQL statement: