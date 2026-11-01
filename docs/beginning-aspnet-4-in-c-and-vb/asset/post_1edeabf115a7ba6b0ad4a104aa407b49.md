
(continued)

| TRANSACTION CLASS MEMBER | DESCRIPTION |
|---|---|
| DependentClone() | With the DependentClone() method, you can create a transaction that depends on the current transaction. |
| TransactionCompleted | TransactionCompleted is an event that is fired when the transaction is completed — either successfully or unsuccessfully. With an event handler object of type TransactionCompletedEventHandler, you get access to the Transaction object and can read its status. |

For demonstrating the features of System.Transaction, the class Utilities inside a separate assembly offers some static methods. The method AbortTx() returns true or false depending on the input from the user. The method DisplayTransactionInformation() gets a TransactionInformation object as parameter and displays all the information from the transaction: creation time, status, local, and distributed identifiers:

```
public static class Utilities
{
    public static bool AbortTx()
    {
        Console.Write("Abort the Transaction (y/n)?");
        return Console.ReadLine() == "y";
    }

    public static void DisplayTransactionInformation(string title,
        TransactionInformation ti)
    {
        if (ti != null)
        {
            Console.WriteLine(title);
            Console.WriteLine("Creation Time: {0}", ti.CreationTime);
            Console.WriteLine("Status: {0}", ti.Status);
            Console.WriteLine("Local ID: {0}", ti.LocalIdentifier);
            Console.WriteLine("Distributed ID: {0}", ti.DistributedIdentifier);
            Console.WriteLine();
        }
    }
}
```

code snippet Utilities/Utilities.cs

## Committable Transactions

The Transaction class cannot be committed programmatically; it does not have a method to commit the transaction. The base class Transaction just supports aborting the transaction. The only transaction class that supports a commit is the class CommittableTransaction.

With ADO.NET, a transaction can be enlisted with the connection. To make this possible, an AddStudent() method is added to the class StudentData that accepts a System.Transactions.Transaction object as second parameter. The object tx is enlisted with the connection by calling the method EnlistTransaction of the SqlConnection class. This way, the ADO.NET connection is associated with the transaction:

```
public void AddStudent(Student student, Transaction tx)
{
    var connection = new SqlConnection(
        Properties.Settings.Default.CourseManagementConnectionString);
    connection.Open();
    try
    {
        if (tx != null)
            connection.EnlistTransaction(tx);
        SqlCommand command = connection.CreateCommand();
        command.CommandText = 'INSERT INTO Students (FirstName, ' +
            'LastName, Company)' +
            'VALUES (@FirstName, @LastName, @Company)';
        command.Parameters.AddWithValue("@FirstName", student.FirstName);
        command.Parameters.AddWithValue("@LastName", student.LastName);
        command.Parameters.AddWithValue("@Company", student.Company);
        command.ExecuteNonQuery();
    }
    finally
    {
        connection.Close();
    }
}
```

code snippet DataLib/StudentData.cs

In the CommittableTransaction() method of the console application TransactionSamples, first a transaction of type CommittableTransaction is created, and information is shown on the console. Then a Student object is created, and this object is written to the database from the AddStudent() method. If you verify the record in the database from outside the transaction, you cannot see the student added until the transaction is completed. In case the transaction fails, there is a rollback, and the student is not written to the database.

After the AddStudent() method is invoked, the helper method Utilities.AbortTx() is called to ask if the transaction should be aborted. If the user aborts, an exception of type ApplicationException is thrown and, in the catch block, a rollback is done by calling the method Rollback() of the Transaction class. The record is not written to the database. If the user does not abort, the Commit() method commits the transaction, and the final state of the transaction is committed:

```
static void CommittableTransaction()
{
    var tx = new CommittableTransaction();
    Utilities.DisplayTransactionInformation("TX created",
        tx.TransactionInformation);

    try
    {
        var s1 = new Student
        {
            FirstName = "Jörg",
            LastName = "Neumann",
            Company = "thinktecture"
        };
        var db = new StudentData();
        db.AddStudent(s1, tx);

        if (Utilities.AbortTx())
        {
            throw new ApplicationException("transaction abort");
        }

        tx.Commit();
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
        Console.WriteLine();
        tx.Rollback();
    }
    Utilities.DisplayTransactionInformation("TX completed",
        tx.TransactionInformation);
}
```

code snippet TransactionSamples/Program.cs

Here, you can see the output of the application where the transaction is active and has a local identifier. The output of the application that follows shows the result with the user choice to abort the transaction. After the transaction is finished, you can see the aborted state:

```
TX created
Creation Time: 7:30:49 PM
Status: Active
Local ID: bdcf1dc-a67e-4ccc-9a5c-cbdf0fe9177:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Abort the Transaction (y/n)? y
Transaction abort

TX completed
Creation Time: 7:30:49 PM
Status: Aborted
Local ID: bdcf1dc-a67e-4ccc-9a5c-cbdf0fe9177:1
Distributed ID: 00000000-0000-0000-0000-000000000000
```

With the second output of the application that you can see here, the transaction is not aborted by the user. The transaction has the status committed, and the data is written to the database:

```
TX Created
Creation Time: 7:33:04 PM
Status: Active
Local ID: 708da71-fa2a-4649-86b4-18b83120f6af:1
Distributed ID: 00000000-0000-0000-0000-000000000000

Abort the Transaction (y/n)? n

TX completed
Creation Time: 7:33:04 PM
Status: Committed
Local ID: 708da71-fa2a-4649-86b4-18b83120f6af:1
Distributed ID: 00000000-0000-0000-0000-000000000000
```

## Transaction Promotion

System.Transactions supports promotable transactions. Depending on the resources that participate with the transaction, either a local or a distributed transaction is created. SQL Server 2005 and 2008 support promotable transactions. So far you have seen only local transactions. With all previous samples, the distributed transaction ID was always set to 0, and only the local ID was assigned. With a resource that does not support promotable transactions, a distributed transaction is created. If multiple resources are added to the transaction, the transaction may start with a local transaction and promote to a distributed transaction as required. Such a promotion happens when multiple SQL Server database connections are added to the transaction. The transaction starts as a local transaction and then is promoted to a distributed transaction.

The console application is now changed in that a second student is added by using the same transaction object tx. Because every AddStudent() method opens a new connection, two connections are associated with the transaction after the second student is added:

```
static void TransactionPromotion()
{
    var tx = new CommittableTransaction();
    Utilities.DisplayTransactionInformation("TX created", tx.TransactionInformation);

    try
    {
        var s1 = new Student
        {
            FirstName = "Jörg",
            LastName = "Neumann",
            Company = "thinktecture"
        };
        var db = new StudentData();
        db.AddStudent(s1, tx);

        var s2 = new Student
        {
            FirstName = "Richard",
            LastName = "Blewett",
            Company = "thinktecture"
        };
        db.AddStudent(s2, tx);

        Utilities.DisplayTransactionInformation("2nd connection enlisted", tx.TransactionInformation);

        if (Utilities.AbortTx())
        {
            throw new ApplicationException("transaction abort");
        }

        tx.Commit();
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
        Console.WriteLine();
        tx.Rollback();
    }

    Utilities.DisplayTransactionInformation("TX finished", tx.TransactionInformation);
}
```

code snippet TransactionSamples/Program.cs

Running the application now, you can see that with the first student added the distributed identifier is 0, but with the second student added the transaction was promoted, so a distributed identifier is associated with the transaction:

```
TX created
Creation Time: 7:56:24 PM
Status: Active
Local ID: 6d2f5ada-32a-40eb-b9d7-cc6aa9a2a554:1
Distributed ID: 00000000-0000-0000-0000-000000000000

2nd connection enlisted
```
