# Isolation

Every transaction should operate as if it is the only transaction in the system.

# Durability

Once a transaction is completed successfully, the updated rows/records must be available for all other transactions on a permanent basis.

# 16.8.2 Transaction Commands

The transaction commands are only used in SQL DML (Data Manipulation Language) that has operations like INSERT, UPDATE and DELETE. That is they change the data. The DDL (Data Definition Language) or DCL (Data Control Language) are used to in creating structure and SQL security.

The transaction commands are as below,

+   - **COMMIT**
+     This command is used to save the changes invoked by the transaction.
+   - **ROLLBACK**
+     This command is used to undo the changes made by transaction.
+   - **SAVEPOINT**
+     With the help of this command one can roll the transaction back to a certain point without rolling back the entire transaction.
+   - **SET TRANSACTION**
+     This command is used to specify characteristics for the transaction. For example, one can specify a transaction to be read only, or read write it. Also helps set the name of transaction.

# 16.8.3 Transaction with ADO.NET

//example to illustrate SQL transaction used in ADO.NET.
Example

```
```csharp
string strConnString = "connectionstring"; // can be taken from Web.config file
SqlTransaction objTrans = null;
using (SqlConnection objConn = new SqlConnection(strConnString))
{
    objConn.Open();
    objTrans = objConn.BeginTransaction();
    SqlCommand objCmd1 = new SqlCommand("insert into tblAuthor values(12, 'Ravi')", objConn);
    SqlCommand objCmd2 = new SqlCommand("insert into tblTechMember(MemberID, TaskID) values(5, 15)", objConn);
}
```
```