# An Example of Transactions

For the transaction example, you'll build a simple business-logic component that transfers data from one bank account to another account. The current balance in the first bank account will be represented by a row in one database, while the other will be represented by a row in another database.

Before beginning, note one important point: You can't have transactions without any resource managers. It's very tempting to assume that you can experiment with transactional component services without actually involving, say, a database, because (as you shall see) none of the methods in the transactional classes make any explicit references to one. However, if you do try to do this, then you will find that your transactions don't actually trouble the system's statistics. Fortunately, you don't need to lay out your hard-earned cash for a copy of SQL Server (nice though that is), because a lightweight (but fully functional) version of SQL Server is available: *SQL Server 2008 Express Edition*, or more simply *SQL Server Express*. In addition, SQL Express is available separately, so you can even work with databases if you use Visual Basic Express.

# Creating the Databases

First, set up the databases. Check whether the Server Explorer tab is visible in Visual Studio (see Figure D-1). If not, then open it by selecting View ▸ Server Explorer. Create a new database in the Data Connections tree.

Right-click Data Connections and select Create New SQL Server Database from the menu. The Create New SQL Server Database dialog appears (see Figure D-2).

Enter the database name (**BankOfWrox**) and select Use Windows Authentication. After clicking OK, you are prompted to create the database if it doesn't exist. You should now see BankOfWrox in the list of data connections (see Figure D-3).

![](bbox=[0.66, 0.355, 0.88, 0.456])

![](bbox=[0.09, 0.529, 0.374, 0.783])

![](bbox=[0.44, 0.625, 0.67, 0.783])

Set up the database. If you open the new node, you will see several other nodes, including Tables. Right-click this and then select Add New Table from the menu. Another dialog should appear (see Figure D-4). Create two columns, Name and Amount, as shown. Make sure that Name is set up to be the primary key. When you click Close, you'll be asked whether you want to save the changes to Table1. Select Yes, and the Choose Name dialog will appear (see Figure D-5).