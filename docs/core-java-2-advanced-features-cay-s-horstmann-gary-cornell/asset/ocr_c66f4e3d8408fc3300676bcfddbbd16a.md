**java.sql.Savepoint 1.4**

- `int getSavepointId()`  
  gets the ID of this unnamed save point, or throws a `SQLException` if this is a named save point.
- `String getSavepointName()`  
  gets the name of this save point, or throws a `SQLException` if this is an unnamed save point.

**java.sql.Statement 1.1**

- `void addBatch(String command) 1.2`  
  adds the command to the current batch of commands for this statement.
- `int[] executeBatch() 1.2`
- `long[] executeLargeBatch() 8`  
  executes all commands in the current batch. Each value in the returned array corresponds to one of the batch statements. If it is non-negative, it is a row count. If it is the value `SUCCESS_NO_INFO`, the statement succeeded, but no row count is available. If it is `EXECUTE_FAILED`, the statement failed.

**java.sql.DatabaseMetaData 1.1**

- `boolean supportsBatchUpdates() 1.2`  
  returns true if the driver supports batch updates.

# 5.10 Advanced SQL Types

Table 5.8 lists the SQL data types supported by JDBC and their equivalents in the Java programming language.

A SQL ARRAY is a sequence of values. For example, in a Student table, you can have a Scores column that is an `ARRAY` of `INTEGER`. The getArray method returns an object of the interface type `java.sql.Array`. That interface has methods to fetch the array values.

When you get a LOB or an array from a database, the actual contents are fetched from the database only when you request individual values. This is a useful performance enhancement, as the data can be quite voluminous.