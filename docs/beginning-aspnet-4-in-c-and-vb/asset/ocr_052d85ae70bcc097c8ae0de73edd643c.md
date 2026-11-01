```
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

# Transaction Promotion

System.Transactions supports promotable transactions. Depending on the resources that participate with the transaction, either a local or a distributed transaction is created. SQL Server 2005 and 2008 support promotable transactions. So far you have seen only local transactions. With all previous samples, the distributed transaction ID was always set to 0, and only the local ID was assigned. With a resource that does not support promotable transactions, a distributed transaction is created. If multiple resources are added to the transaction, the transaction may start with a local transaction and promote to a distributed transaction as required. Such a promotion happens when multiple SQL Server database connections are added to the transaction. The transaction starts as a local transaction and then is promoted to a distributed transaction.