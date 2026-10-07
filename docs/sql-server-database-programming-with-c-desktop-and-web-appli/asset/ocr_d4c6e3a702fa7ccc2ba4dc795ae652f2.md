# SQL Server Database Programming with C#

![](bbox=[0.334, 0.085, 0.665, 0.365])

**FIGURE 4.23** The relationship between LINQ to DataSet and ADO.NET 2.0

model of a relational database is mapped to an object model expressed in the programming language of the developer with three layers. When the application runs, LINQ to SQL translates into SQL the language-integrated queries in the object model and sends them to the database for execution. When the database returns the results, LINQ to SQL translates them back to objects that you can work with in your programming language.

Two popular LINQ SQL Tools, SQLMetal and Object Relational Designer, are widely used in developing applications using LINQ to SQL. The SQLMetal provides a DOS-like template with a black-white window. Developers using Visual Studio typically use the Object Relational Designer, which provides a graphical user interface for implementing many of the features of the LINQ to SQL.

# 4.3.4 OVERVIEW OF LINQ TO ENTITIES

LINQ to Entities belongs to LINQ to ADO.NET and is a sub-component of LINQ to ADO.NET. Through the Entity Data Model we discussed in 3.4.8.1 in Chapter 3, ADO.NET 3.5 exposes entities in the .NET environment. This makes the object an ideal target for Language-Integrated Query (LINQ) support. Furthermore, LINQ to ADO.NET includes LINQ to Entities. LINQ to Entities enables developers to write queries against the database from the same language used to build the business logic. Figure 4.24 shows the relationship between LINQ and the Entity Framework, ADO.NET 2.0, and the data store.

It can be found that the Entities and Entity Data Model (EDM) released by ADO.NET 3.5 locates at the top of the LINQ to Entities, and they are converted to the logical model by the Mapping Provider and interfaced to the data components as Data Providers defined in ADO.NET 2.0. The bottom components used for this model are all 'old' components that work for the ADO.NET 2.0.

Most applications are currently written on the relational databases and they are compatible with ADO.NET 2.0. At some point, these applications will interact with the data represented in a relational form. Database schemas are not always ideal for building applications, and the conceptual models of applications differ from the logical models of databases. The Entity Data Model (EDM)