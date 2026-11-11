When you supply a string argument, you refer to the column in the result set with that name. For example, rs.getDouble("Price") returns the value of the column with label Price. Using the numeric argument is a bit more efficient, but string arguments make the code easier to read and maintain.

Each get method makes reasonable type conversions when the type of the method doesn't match the type of the column. For example, the call rs.getString("Price") converts the floating-point value of the Price column to a string.

| java.sql.Connection 1.1 |
|---|
| • `Statement createStatement()`<br>creates a Statement object that can be used to execute SQL queries and updates without parameters. |
| • `void close()`<br>immediately closes the current connection and the JDBC resources that it created. |

| java.sql.Statement 1.1 |
|---|
| • `ResultSet executeQuery(String sqlQuery)`<br>executes the SQL statement given in the string and returns a ResultSet object to view the query result. |
| • `int executeUpdate(String sqlStatement)`<br>`long executeLargeUpdate(String sqlStatement)` 8<br>executes the SQL INSERT, UPDATE, or DELETE statement specified by the string. Also executes Data Definition Language (DDL) statements such as CREATE TABLE. Returns the number of rows affected, or 0 for a statement without an update count. |
| • `boolean execute(String sqlStatement)`<br>executes the SQL statement specified by the string. Multiple result sets and update counts may be produced. Returns true if the first result is a result set, false otherwise. Call getResultSet or getUpdateCount to retrieve the first result. See Section 5.5.4, “Multiple Results,” on p. 321 for details on processing multiple results. |