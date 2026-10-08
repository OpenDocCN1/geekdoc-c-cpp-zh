# 22.5 Querying a Database with LINQ 945

The IDE displays a Choose Data Source dialog, select Microsoft Server Database File and click Continue.) For the Data source field, if Microsoft Server Database File (SqlClient) is not displayed, click Change..., select Microsoft Server Database File (SqlClient) and click OK. Next, click Browse... to the right of the Database file name to locate and select the Books.mddf in the Directories included with this chapter. You can Test whether the IDE can connect to the database through SQL Server. Click OK to create the connection. 22.14 shows the Connection string for Books.mddf database. This contains the information that the ADO.NET Entity Framework requires to connect to the information at runtime. Click Next > A dialog will appear if you like to add the database file to your project. Click Yes to move to the next step.

![](bbox=[0.248, 0.349, 0.722, 0.676])

22.14 | Choose Your Data Connection after selecting Books.mddf.

+   4. Choosing the Entity Framework Version. In the Choose Your Version step, the Entity Framework 6.x (Fig. 22.15), then click Next. This adds the latest version of the Entity Framework to your project.

+   5. Choosing the Database Objects to Include in the Model. In the Choose Your Database Objects and Settings step, you will specify which parts of the database that should be used in the ADO.NET Entity Data Model. Select the Tables node as shown in Fig. 22.16, then click Finish. At this point, the IDE will download the Entity Framework 6.x templates you need and add them to your project. You may see one or more Security Warning dialogs—Visual Studio displays these when you attempt to download content in your projects. Click OK to dismiss each dialog. Warnings are intended primarily for cases in which a Visual Studio template is downloaded from an untrusted website.