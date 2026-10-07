
Queries that perform aggregation functions over a source of elements first iterate over those elements. Examples of queries are Count, Max, Average, and First. These execute without an explicit foreach statement because the query itself must use foreach to return a result. Note that these types of queries return a single value, rather than an Enumerable collection. To force the execution of any query and cache its results, you can call the ToList<TSource> or ToArray<TSource> methods. You can also force execution by putting the loop immediately after the query expression. By calling ToList or ToArray you also cache all the data in a single collection object.

## 4.3 THE LINQ ARCHITECTURE AND COMPONENTS OF LINQ

LINQ is composed of three major components: LINQ to Objects, LINQ to ADO.NET and LINQ to XML. A detailed organization of the LINQ can be written as:

- 1. LINQ to Objects
- 2. LINQ to ADO.NET (LINQ to DataSet, LINQ to SQL and LINQ to Entities)
- 3. LINQ to XML

All of the components are located at the different namespaces provided by .NET Framework 3.5, which is shown in Figure 4.21. A typical LINQ architecture is shown in Figure 4.22. Now let's give a brief introduction for each component in LINQ.

| Namespace | Purpose |
|---|---| |
| System.Linq | Classes and interfaces that support LINQ queries are located at this namespace |
| System.Collections.Generic | All components related to IEnumerable and IEnumerator<T> are located at this namespace (LINQ to Objects) |
| System.Data.Linq | All classes and interfaces related to LINQ to SQL are defined in this namespace |
| System.XML.Linq | All classes and interfaces related to LINQ to XML are defined in this namespace |
| System.Data.Linq.Mapping | Map a class as an entity class associated with a physical database |

FIGURE 4.21 LINQ-related namespaces.

![](img/d59a47501d0a20fc0460a49c469c6fb7_146_0.png)

FIGURE 4.22 A typical LINQ architecture

# Introduction to Language Integrated Query (LINQ) 119

### 4.3.1 OVERVIEW OF LINQ TO OBJECTS

LINQ to Objects refers to the use of LINQ queries with any IEnumerable or IEnumerable<T> collection directly, without the use of an intermediate LINQ provider or API such as LINQ to SQL or LINQ to XML. The actual LINQ queries are performed using the Standard Query Operator that are static methods of the System.Linq.Enumerable class that you use to create LINQ to Objects. You can use LINQ to query any enumerable collections such as List<T>, Array, or Dictionary<TKey, TValue>. The query may be de-defined or returned by a .NET Framework API.

In a basic sense, LINQ to Objects represents a new approach to collections, which includes arrays and in-memory data. In the process, you had to write complex loops that specified how to retrieve data from a collection. In the LINQ approach, you write declarative code that describes what you want to retrieve.

In addition, LINQ queries offer three main advantages especially when filtering multiple conditions:

- 1) They are more concise and readable, especially when filtering multiple conditions.
- 2) They provide powerful filtering, ordering, and grouping capabilities with a minimum of application code.
- 3) They can be ported to other data sources with little or no modification.

In general, the more complex the operation you perform on the data, the more beneficial it will be to use LINQ instead of traditional iteration techniques.

### 4.3.2 OVERVIEW OF LINQ TO DATASET

LINQ to Data belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Data makes it easier and faster to query data cached in a DataSet object. Specifically, LINQ to Data simplifies querying by enabling writers to query using the programming language itself instead of using a separate query language. This is especially useful for Visual Studio developers, who can take advantage of the compile-time syntax checking, static typing, and IntelliSense support provided by Visual Studio in their queries.

LINQ to Data can also be used to query data that has been consolidated from one or more data sources, and handled as locally aggregated data and middle-tier caching in Web applications. In particular, generic reporting, analysis, and business intelligence applications require this method of manipulation.

The LINQ to Data functionality is primarily extended through the extension methods in the DataRows and DataTable classes. LINQ to DataSets is built on and uses the existing ADO.NET 2.0 architecture, and is not meant to replace ADO.NET 2.0 in application code. The relationship of LINQ to DataSet to ADO.NET 2.0 will continue to function in a LINQ to DataSet relationship. The data store can be illustrated in Figure 4.23.

It can be found from Figure 4.23 that LINQ to Data is built upon ADO.NET 2.0 and uses all its components, including Connection, Command, DataAdapter and DataReader. The advantage of this structure is that all developers using ADO.NET 2.0 continue database implementations without development problems.

### 4.3.3 OVERVIEW OF LINQ TO SQL

LINQ to SQL belongs to LINQ to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to SQL is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

Two popular LINQ SQL Tools, SQLMetal and Object Relational Designer, are widely used in developing applications using LINQ to SQL. The SQLMetal provides a DOS-like template with a black-white window. Developers using Visual Studio typically use the Object Relational Designer, which provides a graphical user interface for implementing many of the features of the LINQ to SQL.

# SQL Server Database Programming with C#

![](img/d59a47501d0a20fc0460a49c469c6fb7_148_0.png)

**FIGURE 4.23** The relationship between LINQ to DataSet and ADO.NET 2.0

### 4.3.4 OVERVIEW OF LINQ TO ENTITIES

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

LINQ to Entities belongs to ADO.NET and it is a sub-component of LINQ to ADO.NET. LINQ to Entities is a component of .NET Framework version 3.5 that provides a runtime-infrastructure for managing relational data as objects. As we discussed in Chapter 3, in LINQ to SQL, the data model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

### 4.3.5 OVERVIEW OF LINQ TO XML

LINQ to XML is a LINQ-enabled, in-memory XML programming interface that enables you to work with XML from within the .NET programming languages. LINQ to XML provides an in-memory XML programming interface that leverages the .NET Language-Integrated Query (LINQ) Framework. LINQ to XML uses the latest .NET Framework capabilities and is comparable to an updated, redesigned Document Object Model (DOM) XML programming interface. This interface had been known as XLing before LINQ.

The LINQ family of technologies provides a consistent experience for objects (LINQ), relational databases (LINQ to SQL), and XML (LINQ to XML).

At this point, we have finished an overview of the LINQ family. Now let's go a little deeper into those topics to get a more detailed discussion for each of them.

## 4.4 LINQ TO OBJECTS

As mentioned in the first section, LINQ to Objects is used to query any sequences or collections that are either explicitly or implicitly contained with IEnumerable sequences or IEnumerable<T> collections. Since any IEnumerable<T> contains a sequence of objects with a data type that is compatible with IEnumerable<T>, there is no need to use any LINQ API like LINQ to SQL to convert or map these collections from an object model to a relational model, and LINQ to Objects can be directly implemented from those collections or sequences to perform the queries.
