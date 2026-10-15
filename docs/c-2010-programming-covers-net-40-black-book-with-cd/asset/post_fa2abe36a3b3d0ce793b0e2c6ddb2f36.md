
## Introducing LINQ to ADO.NET

LINQ to ADO.NET helps you to query on any ADO.NET object using LINQ programming model. It consists of two separate technologies, LINQ to DataSet and LINQ to SQL.

The first component of LINQ to ADO.NET is LINQ to DataSet. This interface is a set of extensions to the standard ADO.NET DataSet programming model that allows DataSet, DataTable, and DataRow for LINQ query expression. LINQ to DataSet provides richer and optimized querying over DataSet.

The second component of LINQ to ADO.NET is LINQ to SQL. This interface allows you to interact with a relational database by removing away the ADO.NET data types through the use of entity classes. LINQ to SQL enables you to directly query the SQL Server database schema.

Figure 27.1 depicts an overview of how LINQ to ADO.NET relates to the high-level programming languages:

![](img/e073a4882197be4ab61103cbe0bcb394_1360_0.png)

Figure 27.1: Displaying an Overview of LINQ to ADO.NET

Let’s now learn about the two important technologies required for LINQ to ADO.NET: LINQ to DataSet and LINQ to SQL.

### LINQ to DataSet

The DataSet is a very useful in-memory representation of data and acts as the core of a wide variety of data based applications. After the data is loaded into the DataSet, there is often a need to perform additional queries on data, which is implemented by LINQ to DataSet.

LINQ to DataSet is an easier and faster way to query data cached in a DataSet object. LINQ to DataSet simplifies querying by enabling you to write queries in the programming language itself. The functions in LINQ to DataSet are performed using operators that allow you to perform LINQ queries on the DataSet. The ADO.NET SQL queries are used to obtain DataSet. LINQ to DataSet allows LINQ queries over any database that can be queried with ADO.NET. You can also use LINQ to DataSet to query over data consolidated from one or more data sources.

The first step before you begin querying a DataSet object by using LINQ to DataSet is to populate the DataSet object. After loading the data in the DataSet object, you can query it.

The LINQ to DataSet functionality is exposed primarily through the extension method in the DataRowExtension and DataTableExtension classes. Figure 27.2 depicts the relationship of LINQ to DataSet:

![](img/e073a4882197be4ab61103cbe0bcb394_1361_0.png)

Figure 27.2: Displaying the Relationship of LINQ to DataSet

### LINQ to SQL

LINQ to SQL is a component of .NET Framework 4.0, and is specifically designed for working with SQL server database. It provides a run-time infrastructure for managing relational data as objects. It allows you to write queries to retrieve and manipulate data from the SQL server. LINQ to SQL supports all the key functions that you would expect while developing SQL applications. You can retrieve the data from the database, insert, update, and delete the information from the table. Your query expression is translated into parameterized SQL code, parameters are created, and the query is executed on the server. LINQ to SQL also supports transactions, views, and stored procedures. It also provides an easy way to integrate data validation and business logic rules into your data model.

LINQ to SQL is an object-relational mapping (ORM) framework that allows the direct one-to-one mapping of Microsoft SQL Server database to .NET classes. With the help of the LINQ to SQL ORM mapping, the classes that match the database table are created automatically from the database itself and you can start using the classes immediately. You can find the practical application of LINQ to SQL in the Immediate Solutions section of this chapter.

### Introducing LINQ to XML

LINQ to XML is a new way to write and read XML data in .NET Framework 4.0. It supplements the standard XML classes in .NET Framework and makes working with XML easier. LINQ to XML provides you with an extra option for creating and querying XML data, which results in simpler code and quicker development. When you are using LINQ to XML, you can query and modify document, and also save the file after modification. It provides a new object model that is easier to work with, and takes advantage of the improvements in C#.

The integration of LINQ with XML enables you to write queries on the in-memory XML document to retrieve collection of elements and attributes. The LINQ capability of LINQ to XML allows you to run queries against XML. LINQ to XML provides an improved XML programming interface.

The System.Xml.Linq namespace contains classes for LINQ to XML. The following are some of the variety of functions that can be performed by using LINQ to XML:

- Loading XML from files or streams
- Serializing XML to files and streams
- Creating XML trees using functional construction
- Querying XML trees using LINQ queries
- Controlling the in-memory XML trees
- Validating the XML trees using XML Schema Definition (XSD)

Let’s now learn about the difference between LINQ to XML and the DOM method and how to work with XML trees in LINQ.

### Difference Between LINQ to XML and DOM Method

XML Document Object Model (DOM) is the current predominant XML programming API. In XML DOM, you build an XML tree in the bottom up direction. The typical way to create an XML tree using DOM is to use the XmlDocument class. LINQ to XML also supports the XmlDocument class approach for constructing an XML tree. It also supports an alternative approach, called the functional construction, which uses the XElement and XAttribute constructors to build an XML tree.

In LINQ to XML, you can directly work with XML elements and attributes. You can create XML elements without using a document object. It also loads the T:System.Xml.Linq.XElement object directly from an XML file. It also serializes the T:System.Xml.Linq.XElement object to a file or a stream. When you compare this with XML DOM, the XML document is used as a logical container for the XML tree. In XML DOM, the nodes, which also include the elements and attributes, are created in the context of an XML document. The use of XML DOM is also complex. For example, if you want to use an element across multiple documents, you must import the nodes across the documents. This kind of complexity is not included in LINQ to XML.

The use of LINQ to XML also simplifies the names and namespaces by eliminating the prerequisite to deal with namespace prefix completely. The use of XML DOM does not let you change the name of node. As a substitute, you have to create a new node and copy all the child nodes to it, which leads to losing the original child identity. LINQ to XML supports whitespace more simply than XML DOM.

### Working with XML Trees in LINQ

LINQ to XML provides a powerful way to create XML elements called functional construction, which has the ability to create an XML tree in a single statement. You need to use the XElement constructor that takes various types of argument for the content to create an XML tree in LINQ. The XElement constructor takes params array type of Object, so that you can pass any number of objects to the constructor. This helps you in using an element that has a complex content. The XAttribute object becomes the attribute of an element.

When you actually create an XML tree, the XElement and XAttribute constructors let you pass the content of the attribute or element as an argument to the constructor. You can pass any number of child elements in them as one of the constructors take a variable number of arguments. It supports any type of object that is a valid child element of an XElement constructor. You should keep in mind the following rules while creating an XML tree in LINQ:

- The string is added as a text content
- An XElement class is added as an attribute
- An XAttribute class is added as an attribute
- You should call the ToString() method for any other type than string

You learn more about working with XML tree in the Immediate Solutions section of this chapter.

### The LinqDataSource Control

The LinqDataSource control enables you to use LINQ in an ASP.NET Web page by setting the properties in the markup text. You can use the LinqDataSource control to create a Web page that retrieves or modifies the
