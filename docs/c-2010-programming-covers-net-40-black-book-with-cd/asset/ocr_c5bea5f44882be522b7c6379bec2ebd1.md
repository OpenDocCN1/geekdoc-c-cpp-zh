# Introducing LINQ to ADO.NET

LINQ to ADO.NET helps you to query on any ADO.NET object using LINQ programming model. It consists of two separate technologies, LINQ to DataSet and LINQ to SQL.

The first component of LINQ to ADO.NET is LINQ to DataSet. This interface is a set of extensions to the standard ADO.NET DataSet programming model that allows DataSet, DataTable, and DataRow for LINQ query expression. LINQ to DataSet provides richer and optimized querying over DataSet.

The second component of LINQ to ADO.NET is LINQ to SQL. This interface allows you to interact with a relational database by removing away the ADO.NET data types through the use of entity classes. LINQ to SQL enables you to directly query the SQL Server database schema.

Figure 27.1 depicts an overview of how LINQ to ADO.NET relates to the high-level programming languages:

![](bbox=[0.17, 0.27, 0.74, 0.6])

Figure 27.1: Displaying an Overview of LINQ to ADO.NET

Let’s now learn about the two important technologies required for LINQ to ADO.NET: LINQ to DataSet and LINQ to SQL.

# LINQ to DataSet

The DataSet is a very useful in-memory representation of data and acts as the core of a wide variety of data based applications. After the data is loaded into the DataSet, there is often a need to perform additional queries on data, which is implemented by LINQ to DataSet.

LINQ to DataSet is an easier and faster way to query data cached in a DataSet object. LINQ to DataSet simplifies querying by enabling you to write queries in the programming language itself. The functions in LINQ to DataSet are performed using operators that allow you to perform LINQ queries on the DataSet. The ADO.NET SQL queries are used to obtain DataSet. LINQ to DataSet allows LINQ queries over any database that can be queried with ADO.NET. You can also use LINQ to DataSet to query over data consolidated from one or more data sources.

The first step before you begin querying a DataSet object by using LINQ to DataSet is to populate the DataSet object. After loading the data in the DataSet object, you can query it.

The LINQ to DataSet functionality is exposed primarily through the extension method in the DataRowExtension and DataTableExtension classes. Figure 27.2 depicts the relationship of LINQ to DataSet: