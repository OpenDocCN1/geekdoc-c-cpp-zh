# 3.4.8.1.2 Entity Data Model Wizard

The Data Model Wizard starts after you add an ADO.NET 3.5 Entity Data Model to your project. The wizard is used to generate an Entity Data Model (EDM). An .edmx file contains the model information. The ADO.NET 3.5 Entity Data Model Designer enables you to view and edit the mappings graphically.

You can select to create an empty model or generate the model from an existing database. Generating the model from an existing database is the recommended practice for this release of the EDM model.

The wizard also creates a source code file that contains the classes generated from the CSDL information encapsulated in the .edmx file. This code is auto-generated and updated when the .edmx file changes.

Depending on your selections, the wizard will help you with the following steps:

+   - Choosing the Model Contents: It is recommended that you select to generate the model from an existing database. The Wizard takes you step by step through the selection of the data source, database, and database objects to include in the EDM.
- Choosing the Database Connection: You can choose an existing connection from the list of connections or click New Database Connection to open the Connection Properties dialog box and create a new connection to the database.
- Choosing your Data Objects: You can select the tables, views, and stored procedures to include in the EDM.

Now let's consider the real part – ADO.NET 3.5 Entity Data Model Designer.

# 3.4.8.1.3 Entity Data Model Designer

The ADO.NET 3.5 Entity Data Model provides visual tools for the creation and editing of an Entity Data Model (EDM).
The ADO.NET Entity Data Model Designer includes the following components:

+   - A visual design surface for creating and editing the conceptual model. You can create, modify, or edit entities and associations.
- An Mapping Details window to view and edit mappings. You can map entity types or associations to database tables and browsers.
- An Entity Model Browser gives you a tree of the EDM.
- Toolbox controls to create entities, associations and inheritance relationships.

The ADO.NET 3.5 Entity Data Model Designer is integrated with the Visual Studio.NET 2008 components. You can view and edit information using the Properties window and errors are reported in the Error List.

Figure 3.42 shows an example of the ADO.NET 3.5 Entity Data Model Designer. Two important functionalities of using the Entity Data Model Designer are.

# 3.4.8.1.3.1 Opening the ADO.NET Entity Data Model Designer

The ADO.NET 3.5 Entity Data Model Designer is designed to work with an .edmx file. The .edmx file is an encapsulation of three EDM metadata artifact files, the Conceptual schema definition language (CSDL), the Store schema definition language (SSDL), and the Mapping specification language (MSL). When you run the EDM Wizard an .edmx file is created and added to your solution. You open the ADO.NET Entity Data Model Designer by double-clicking on the .edmx file in the Solution Explorer.