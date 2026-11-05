block that is not supposed to throw any exception. Do not catch any exception that cannot be handled and avoid rethrowing exceptions unnecessarily as it is very expensive.

# Prevent unnecessary database hit

One of the most useful of all features of ADO.NET is that one can attach messages to each row of data in a DataSet object. The SqlDataAdapter class attaches error messages to the rows of a DataSet if a specific database action has not been successfully completed. Then one can check whether there are any errors in a DataSet prior to sending the same for updating the database using the HasErrors property of the DataSet instance. This, if used judiciously, can prevent an unnecessary database hit. Please refer to the code snippet that follows,

```
DataSet newDataSet = previousDataSet.GetChanges(DataRowState.Modified);
if (newDataSet.HasErrors)
{
    // If there are errors take appropriate action
}
else
{
    // Necessary code to update the database
}
```

# 16.8 Transaction in ADO .NET

A transaction is a single unit of work which means either ALL or NONE. If a transaction is successful, all of the data operations are committed (saved) and become a durable part of the database. If a transaction encounters errors/exceptions and must be canceled or rolled back, then all of the data modifications/operations need to be removed.

Database transaction takes a database from one consistent state to another. At the end of the transaction the system must be in the prior state if the transaction fails or the status of the system should reflect the successful completion if the transaction goes through.

# 16.8.1 Properties of Transaction

# Atomicity

A transaction consists of many steps. When all the steps in a transaction get completed, it will get reflected in DB or if any step fails, all the transactions are rolled back.

# Consistency

The database will move from one consistent state to another, if the transaction succeeds and remains in the original state, or if the transaction fails.