> NOTE
> The String data type does not specify the kind of Unicode to use. The designer must specify the appropriate kind of Unicode from the type system hosting EDM.

# Entity Types

An entity type in EDM is the design template for a data type in the application domain. In a schema, the entity type has a name, properties, and a key that identifies the data type when instantiated by an application code. After it has been schematically defined, the entity type becomes an operational unit for application development each possessing a unique identity.

# Complex Types

The complex type in the EDM is a data type with internal structure, but does not contain the key property. It is used to implement a property that has internal properties of its own.
Sometimes, we need to put constraints to restrict certain properties of an entity. To do this, EDM provides Type constraints. Let’s explore the type constraints next.

# Type Constraints

In EDM, we can put certain constraints over the properties of entity types. Constraints restrict the possible values of a property and verify that the assigned value not only corrects the data types, but also checks that it is working according to the business requirement of the application. Some of the main constraints are as follows:

+   - Nullable constraint — Specifies whether the value of the property can be unassigned
+   - MaxLength constraint — Limits the length of string properties

Entity Framework also provides certain tools to help in working with models, which we describe next.

# Data Model Tools

ADO.NET Entity Framework allows a user to bring data from efficient storage engines, such as SQL Server, to object-oriented programming. Many developers implement complicated data access codes to move data between applications and the database. ADO.NET Entity Framework provides the following tools that help us to develop applications with EDM:

+   - ADO.NET Entity Data Model Item Template — Refers to the template that is available for Visual Basic (VB) and C# projects, and ASP.NET website and Web application projects. It is basically used to launch Entity Data Model Wizard.
+   - Entity Data Model Wizard — Generates EDM from an existing database and also adds a connection string to the App.Config or Web.Config file, and configures a single file generator to run on the conceptual model contained in the .edmx file, which encapsulates generated EDM through the wizard. A conceptual model defined in an .edmx file helps to generate C# code.
+   - The ADO.NET Entity Data Model Designer — Enables us to open an .edmx file in the designer, and creates entities and map entities to database tables and columns through some visual tools included with EDM Designer.
+   - EDMGen.exe — Refers to the command tool that can be used to generate models and perform other functions on EDM metadata files such as validating existing models.

All data types in EDM are supported by LINQ and Entity SQL. This is achieved through Object Services. Now, let’s understand Object Services in detail.

# Understanding Object Services

In Entity Framework, Object Services is a service that supports both LINQ and Entity SQL queries for all the types defined in EDM. Object Services return data as objects including any changes in the object back to the data store. The support of LINQ and Entity SQL queries makes the Object Services capable of performing the QUERY, INSERT, UPDATE, and DELETE data operations. This service is also capable of tracking changes, binding objects to controls, and handling concurrency.