
SQL Server Database Programming with C#

## II. MULTIPLE CHOICE QUESTIONS

7. One can create foreign keys between tables
a. Before any table can be created
b. When some tables are created
c. After all tables are created
d. With no limitations

8. To create foreign keys between tables, first one must select the table that contains a key and then select another table that has ____
a. Primary, foreign
b. Primary, primary
c. Foreign, foreign
d. Foreign, foreign

9. The data type varchar(50) in SQL database is a string with ____
a. Limited length to 50
b. Fixed length of 50
c. Certain number of letters
d. Varying length

10. For data tables in SQL Server, a blank must be ____.
a. Indexed by NULL
b. Kept as a blank
c. Either by NULL or a blank
d. Ind by NULL

## III. EXERCISES

1. What are the advantages of using an integrated database approach over a file processing approach?
2. Define entity integrity and referential integrity. Describe the reasons for enforcing these rules.
3. Entities can have three types of relationships: can be one-to-one, one-to-many, and many-to-many. Draw ER diagrams to illustrate each type of relationship.
4. List all steps to create foreign keys between data tables for the SQL Server 2019 database in SQL Server Management Studio. Illustrate those steps using a real example.
5. List all steps to create foreign keys between data tables for the SQL Server 2019 database in SQL Server Management Studio. Illustrate those steps using a real example.

![](img/d59a47501d0a20fc046a49c6fb70.png)

# 3 Introduction to ADO

It has been a long story for developers to implement sophisticated data processing techniques to enhance data operations. The evolution of data access has been a long process, predominantly focusing on how to deal with relational data in a more flexible manner. The methodology has been focused on Microsoft-based APIs, such as ODBC, OLEDB, Data Access Objects (DAO) and Remote Data Objects (RDO), in addition to many non-Microsoft-based APIs. These APIs did not bridge the gap between object-oriented and semi-structured (XML) data across multiple languages and are challenging and have opportunities for complete architecture. ADO.NET is considered a good solution for the relational database API which was introduced with Visual Studio 2005. The latest version of ADO.NET is 4.0, which has released with .NET Framework 4.0 and Visual Studio. In this chapter, we will provide a detailed review of the history of ADO.NET, and then a full discussion about the components and architectures of ADO.NET. Finally, we introduce some new features and components.

## 3.1 THE ADO AND ADO.NET

ActiveX Data Object (ADO) was developed on Object Linking and Embedding (OLE) and Component Object Model (COM) technologies. COM is used by developers to create reusable software components, link applications and take advantage of Windows services. In recent decades, ADO has been the preferred interface for Visual Basic programmers to access various data sources. The development of data access methods can be traced back to the mid-1990s with Data Access Object (DAO); this was then followed by Remote Data Object (RDO), which is based on Open Database Connectivity (ODBC). The late 1990s saw the development of ADO, which is based on OLEDB. ADO.NET is the latest version of ADO and is based principally on the .NET Framework 4.0. Common Language Runtime provides bi-directional, transparent integration with COM. This means that ADO.NET applications and components can use functionality from each system. However, ADO.NET provides developers with a significant number of benefits, including a more robust security model, automatic memory management native support and Integrated Query (LINQ). For new developments, ADO.NET is highly recommended as a preferred technology because of its powerful runtime environment. This chapter will provide a detailed introduction to ADO.NET and its components, and these components will be utilized for the rest of the book.

In this chapter, you will:

- Learn the basic classes in ADO.NET and its architecture
- Learn the different ADO.NET data providers
- Learn about the Connection and Command components
- Learn about the Parameters collection
- Learn about the DataAdapter and DataReader components
- Learn about the DataSet and DataTable components
- Learn about ADO.NET Entity Framework (EF)
- Learn about ADO.NET Entity Framework Tools (EFT)
- Learn about ADO.NET Entity Data Model (EDM)

First let's have a closer look at ADO.NET and have a global picture of its components.

## 3.2 OVERVIEW OF ADO.NET

ADO.NET is a set of classes that exposes access services to Microsoft .NET programming. ADO.NET provides a rich set of components for creating distributed, data-sharing applications. It is an integral part of the .NET framework, providing access to relational, XML, and application data. ADO.NET supports a variety of development needs, including the creation of front-end database classes and middle-tier business objects by applications, tools, languages, or Internet browsers.

All ADO.NET classes are located at the System.Data namespace with two files named System.Data and System.Xml. When compiling code use the System.Data namespace, reference both System.Data and System.Xml.

Basically speaking, ADO.NET provides a set of classes to support you to develop database applications and enable you to connect to a data source to retrieve, manipulate and update data with your database. The classes provided by ADO.NET are core to develop a professional data-driven application and can be divided into the three major components:

- Data Provider
- DataSet
- DataTable

These three components are located at the different namespaces. The DataSet and the DataTable classes are located at the different namespaces based on the types of the Data Providers.

Data Provider contains four classes: Connection, Command, DataAdapter and DataReader. These four classes are used to perform different functionalities to help you to:

1) Set a connection between your project and the data source using the Connection object
2) Execute data queries to retrieve, manipulate and update data using the Command object
3) Move the data between your DataSet and your database using the DataAdapter object
4) Perform data queries from the database (read-only) using the DataReader object

The DataSet class is considered as a table and can contain multiple tables. These data tables are only a mapping to real data in your database. But these tables can also be used separately without connecting to the DataSet. In this case, each data table can be considered as a DataTable object.

The DataSet and DataTable classes have no direct relationship with the Data Provider class; therefore they are often called Data Provider-independent components. Four classes, Connection,
