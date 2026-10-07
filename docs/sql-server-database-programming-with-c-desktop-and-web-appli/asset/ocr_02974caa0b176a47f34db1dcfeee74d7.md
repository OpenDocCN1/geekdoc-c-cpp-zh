# SQL Server Database Programming with C#

Some older database systems only support ODBC as the access technique, which include older versions of SQL Server and Oracle as some third-party database as Sybase.

# 3.4.1.2 The OLEDB Data Provider

The System.Data.OleDb namespaces hold all classes used by the .NET Framework 2.0 Data Provider for OLE DB. The .NET Framework Data Provider for OLE DB describes a collection of classes to access an OLE DB database source in the managed space. Using OleDbDataAdapter, you can fill a memory-resident DataSet that you can use to query and update the data source. The following Data Providers support:

+   - Microsoft Access
- SQL Server (7.0 or later)
- Oracle (9 or later)

One advantage of using the OLEDB.NET Data Provider is to allow users to develop a generic data-application. The so-called generic application means you can use the OLEDB.NET Data Provider to access any data source such as Microsoft Access, SQL Server, Oracle and other data source that support the OLEDB.

Figure 3.4 shows the compatibility between the OLEDB Data Provider and the OLE DB.NET Provider.

# 3.4.1.3 The SQL Server Data Provider

This Data Provider access to a SQL Server version 7.0 or later database using its internal protocol. The functionality of the data provider is designed to be similar to that of the .NET Framework data providers for OLE DB, ODCB, and Oracle. All classes related to this Provider are defined in a DLL file and is located at the System.Data.SqlClient namespace. Although Microsoft provides different Data Providers to access the data in SQL Server database, such as the ODCB and OLE DB, for the sake of optimal operations, it is highly recommended to use this Provider to access the data in an SQL Server data source.

As shown in Figure 3.4, this Data Provider is a new version and it can only work for the SQL Server version 7.0 and later. If an older version of SQL is used, you need to use either OLE DB.NET or SQLOLEDB Data Provider.

# 3.4.1.4 The Oracle Data Provider

This Data Provider is an add-on to the .NET Framework that provides access to the Oracle database. All classes related to this Data Provider are located in the System.Data.Oracle namespace. This provider relies upon Oracle Client Interfaces by the Oracle Client Software. You need to install the Oracle client on your computer to use this Data Provider.
Microsoft provides multiple ways to access the data stored in an Oracle database, such as Microsoft ODBC for Oracle and OLE DB, you should use this Oracle Data Provider to access the data in an Oracle data source since this one the most efficient way to access the Oracle database.

This Data Provider can only work for the recent versions of the Oracle database such as 8.1.7 and For older versions of the Oracle database, you need to use MSDAORA or an OLE DB.NET.

| Provider Name | Descriptions |
|---|---|
| SQLOLEDB | Used for Microsoft SQL Server 6.5 or earlier |
| Microsoft.Jet.OLEDB.4.0 | Use for Microsoft JET database (Microsoft Access) |
| MSDAORA | Use for Oracle 7 or later database |

FIGURE 3.4 The compatibility between the OLEDB and OLEDB.NET.