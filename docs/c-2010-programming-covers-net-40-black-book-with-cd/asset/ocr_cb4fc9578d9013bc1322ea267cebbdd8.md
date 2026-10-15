The EDM includes tables, views, and stored procedures that we have selected at the time of selecting database objects. The Model.edmx file created by the wizard must be added to the App_Code folder of the ASP.NET website project. If we select to relocate the .edmx file to another directory, then the model is not supported by the EDM build provider for ASP.NET. Now, let’s understand how to work with ADO.NET Entity Data Model Designer.

# Working with Entity Data Model Designer

ADO.NET Entity Data Model Designer works with an .edmx file that is an encapsulation of the CSDL, the SSDL, and the MSL files. This .edmx file is created and added to our project after the creation of EDM. We can make changes to the EDM through the .edmx file by using ADO.NET Entity Data Model Designer. To open the EDM designer, double-click the Model.edmx file in Solution Explorer, as shown in Figure 22.13:

![](bbox=[0.365, 0.255, 0.565, 0.38])

Figure 22.13: Displaying the Model.edmx File in the App_Code Folder

The EDM designer window appears (Figure 22.14). It provides a design surface for editing the conceptual model that provides functionalities to work with entities. Let’s now learn about the following windows:

+   - Model Browser
+   - Mapping Details

# Using the Entity Model Browser Window

The Model Browser window displays the information in two nodes. The first node displays the details of the conceptual model. We can expand the underlying nodes to view all entity types and associations included in the model. The second node displays the details of targeted database models. Figure 22.14 displays parts of database tables, views, and stored procedures that are used in the model:

![](bbox=[0.32, 0.58, 0.62, 0.825])

Figure 22.14: Viewing the Model.edmx File with Model Browser Window

> NOTE
> You can view the Model Browser window by clicking View → Other Windows → Entity Data Model Browser option from the menu bar.