# Introduction to ADO.NET

In the following sections, we will discuss the Entity Data Model and how to use these Entity Data Tools to create, build and develop the Entity Data Model and implement it in your actual data-driven applications.

First's take a closer look at the ADO.NET 3.5 Entity Data Model.

# 3.4.8.1 ADO.NET 3.5 Entity Data Model

ADO.NET 3.5 Entity Data Model (EDM) is a data model for defining application data as sets of entities and relationships with common runtime CLR type and storage structures can be mapped. This enables developers to create data accesses by programming against conceptual model instead of programming directly against a relational storage schema. The following tools are designed to help you work with the EDM:

+   - The ADO.NET 3.5 Entity Data Model item is available for Visual C# project type, and ASP.NET Web Site and Web Application projects, launches the Entity Data Model Wizard.
- The Entity Data Model Wizard generates the EDM, which is encapsulated in an .edmx file. The wizard also adds a connection string to the App.Config or Web.Config file and configures a single-file generator to the conceptual model in the .edmx file. This single-file generator generates C# or VB code from the conceptual model defined in the .edmx file.
- The ADO.NET Data Model Designer provides visual tools to view and edit the EDM graphically. You can open an .edmx file to design and create entities and map entities to tables and columns.
- EdGen is a command-tool that can be used to also generate models, validate existing models, and perform other functions on your EDM metadata.

In the following sections we will provide a detailed discussion for each of these tools.

# 3.4.8.1.1 Entity Data Model Item Template

ADO.NET 3.5 Entity Data Model item template is the starting point for the Entity Data Model tools. The ADO.NET 3.5 Entity Data Model template is available for Visual C# and Visual Basic project types. It can be added to Console Application, Windows Application, Class Library, ASP.NET Web Service Application, ASP.NET Web Application, or ASP.NET Web Sites. You can add ADO.NET 3.5 Entity Data Model items to the project, with each item containing files that were generated from a different database and/or tables within the same.

When you add the ADO.NET 3.5 Entity Data Model item template to your project, Visual Studio:

+   - Adds references to the System.Data,System.Entity,System.Core,System.Security, and System.Runtime.Serialization assemblies if the project does not have them.
- Starts the Entity Data Model Wizard. The wizard is used to generate an Entity Data Model (EDM) from an existing database. The wizard creates an .edmx file, which contains the model information. You can use the .edmx file in the ADO.NET Entity Data Designer to view or modify the model.
- Creates a source code file that contains the classes generated from the conceptual model. The source code file is auto-generated, is updated when the .edmx file changes, and is compiled as part of the project.

Next let us consider the Entity Data Model Wizard.