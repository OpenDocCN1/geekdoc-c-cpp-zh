Windows 2000 Component Services. The OLE DB .NET data provider does not support OLE DB 2.5 interfaces. OLE DB providers that require support for OLE DB 2.5 interfaces will not function properly with the OLE DB .NET data provider. This includes the Microsoft OLE DB provider for Exchange and the Microsoft OLE DB provider for Internet Publishing. The OLE DB .NET data provider requires the installation of MDAC 2.6 or later. To use this provider, you need to include the `System.Data.OleDb` namespace in your application.

# THE DATASET COMPONENT

The DataSet is central to supporting disconnected, distributed data scenarios with ADO.NET. The DataSet is a memory-resident representation of data that provides a consistent relational programming model regardless of the data source. The DataSet represents a complete set of data, including related tables, constraints, and relationships among the tables; basically, it’s like having a small relational database residing in memory.

> > Because the DataSet contains a lot of metadata, you need to be careful about how much data you try to stuff into it, as it consumes memory.

The methods and objects in a DataSet are consistent with those in the relational database model. The DataSet can also persist and reload its contents as XML, and its schema as XSD. It is completely disconnected from any database connections, so it is totally up to you to fill it with whatever data you need in memory.

Ever since ADO.NET 2.0, several new features have been added to the DataSet and the DataTable classes, as well as enhancements to existing features. The features covered in this section are as follows:

+   - The binary serialization format option
+   - Additions to make the DataTable more of a standalone object
+   - The capability to expose DataSet and DataTable data as a stream (DataReader), and to load stream data into a DataSet or DataTable

# DataTableCollection

An ADO.NET DataSet contains a collection of zero or more tables represented by DataTable objects. The DataTableCollection contains all of the DataTable objects in a DataSet.

A DataTable is defined in the System.Data namespace and represents a single table of memory-resident data. It contains a collection of columns represented by the DataColumnCollection, which defines the schema and rows of the table. It also contains a collection of rows represented by the DataRowCollection, which contains the data in the table. Along with the current state, a DataRow retains its original state and tracks changes that occur to the data.

# DataRelationCollection

A DataSet contains relationships in its DataRelationCollection object. A relationship (represented by the DataRelation object) associates rows in one DataTable with rows in another DataTable. The relationships in the DataSet can have constraints, which are represented by UniqueConstraint and ForeignKeyConstraint objects. It is analogous to a JOIN path that might exist between the primary and foreign key columns in a relational database. A DataRelation identifies matching columns in two tables of a DataSet.

Relationships enable you to see what links information within one table to another. The essential elements of a DataRelation are the name of the relationship, the two tables being related, and the related columns.