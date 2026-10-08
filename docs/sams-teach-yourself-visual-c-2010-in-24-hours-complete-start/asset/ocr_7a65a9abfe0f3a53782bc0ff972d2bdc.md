version of the OLTP database, which you can install from http://msftdbprodsamples.codeplex.com/.

# Understanding ADO.NET

The ADO.NET library is a rich framework enabling you to build applications that can retrieve and update information in relational databases. In keeping with the ideals of language and platform independence, ADO.NET is built upon the idea of data providers. Each database system that ADO.NET supports (such as SQL Server, Oracle, and DB2) has a data provider that implements the mechanisms for connecting to a database, executing queries, and updating data. Because each provider implements the same interfaces, you can write code that is independent of the underlying database.

One of the primary classes in ADO.NET is the DataSet, which represents a portion of the database. A DataSet does not require a continuous connection to the database, enabling you to work in a disconnected manner. To update the database and the DataSet, you periodically reconnect the DataSet to its parent database and perform any updates required.

By the Way

**ADO.NET Data Providers**
An ADO.NET data provider encapsulates the logic needed for connecting to a database, executing commands, and retrieving results. It provides a lightweight layer between the underlying data source and your application code.
The .NET Framework currently ships with five data providers, each in their own namespace:
► Data Provider for SQL Server (System.Data.SqlClient)
► Data Provider for OLE DB (System.Data.OleDb)
► Data Provider for ODBC (System.Data.Odbc)
► Data Provider for Oracle (System.Data.OracleClient)
► EntityClient Provider (System.Data.EntityClient)
Even though SQL Server and Oracle both support OLE DB, you should use the specific SQL Server or Oracle providers because they are optimized for those database systems.

To accomplish all this, the DataSet must represent database tables and the relationships between those tables. The collection of database tables is available through the Tables property, with each table represented as a DataTable instance. The