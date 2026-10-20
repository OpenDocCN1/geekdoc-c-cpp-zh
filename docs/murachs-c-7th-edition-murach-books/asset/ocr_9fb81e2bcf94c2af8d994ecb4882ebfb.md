# A SQL Server SELECT statement that uses a parameter

```
SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
WHERE CustomerID = @CustomerID
```

# An OLE DB or ODBC SELECT statement that uses a parameter

```
SELECT CustomerID, Name, Address, City, State, ZipCode
FROM Customers
WHERE CustomerID = ?
```

# A SQL Server INSERT statement that uses parameters

```
INSERT INTO Customers (Name, Address, City, State, ZipCode)
VALUES (@Name, @Address, @City, @State, @ZipCode)
```

# A SQL Server DELETE statement that uses parameters

```
DELETE FROM Customers
WHERE CustomerID = @CustomerID
AND Name = @Name
AND Address = @Address
AND City = @City
AND State = @State
AND ZipCode = @ZipCode
```

# Description

+   - A *parameter* lets you place variable information into a SQL statement.
+   - When you use a parameter in the WHERE clause of a SELECT statement, the resulting query is often called a *parameterized query* because the results of the query depend on the values of the parameters.
+   - You can also use parameters in INSERT or UPDATE statements to provide the values for the database row or rows to be inserted or updated. Likewise, you can use parameters in a DELETE statement to indicate which row or rows should be deleted.
+   - You can also use parameters in UPDATE and DELETE statements to provide for concurrency.
+   - To use parameters, you code a SQL statement with placeholders for the parameters. Then, you create a parameter object that defines each parameter, and you add it to the Parameters collection of the command object that contains the SQL statement.
+   - The placeholder for a parameter in a SQL Server command is a *named variable* whose name begins with an at sign (@). In most cases, you’ll give the variable the same name as the column it’s associated with.
+   - If you’re using the OLE DB or ODBC provider, you code the placeholder for a parameter as a question mark. The question mark simply indicates the position of the parameter.