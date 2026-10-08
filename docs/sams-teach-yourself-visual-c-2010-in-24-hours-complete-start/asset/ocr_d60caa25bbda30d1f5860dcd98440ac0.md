The Entity Framework then translates this domain model, commonly called a **conceptual model**, to data source-specific commands. This approach enables you to develop your application without being concerned about dependencies on a particular data source.

When the domain model has been defined, the Entity Framework then maps relational tables, columns, and foreign key constraints to classes in the logical model. This approach enables a great deal of flexibility to define and optimize the logical model. The classes generated are partial classes, enabling you to extend them easily.

To access or modify data through the Entity Framework, you execute queries against the conceptual model to return objects through one of the following methods:

+   LINQ to Entities provides LINQ support for querying directly against the conceptual model. Both the Entity Framework and LINQ can then use the objects returned from a LINQ to Entities query.

+   Entity SQL, which is a data source-independent version of SQL that works directly with the conceptual model.

+   Query builder methods, which enable you to create Entity SQL queries using a similar syntax to the LINQ extension methods.

To make creating entity models easier, Visual Studio 2010 includes the Entity Data Model Designer, shown in Figure 24.1. The model shown in Figure 24.1 was created from the AdventureWorksLT database you used in Hour 15, “Working with Databases.”

# **FIGURE 24.1**
Entity data model designer

![](bbox=[0.25, 0.62, 0.82, 0.89])