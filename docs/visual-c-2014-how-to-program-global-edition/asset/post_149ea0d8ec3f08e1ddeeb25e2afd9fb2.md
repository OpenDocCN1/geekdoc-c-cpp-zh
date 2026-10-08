
2. Choosing the Model Contents. The Choose Model Contents step in the Entity Data Model Wizard dialog (Fig. 22.12) enables you to specify the entity data model's contents. In these examples will consist of data from the Books data-base, so select EF Designer from database and click Next > display the Choose Data Connection step.

![](img/57baed2319be0bb1b5f98674846f2711_944_0.png)

Fig. 22.12 | Entity Data Model Wizard dialog's Choose Model Contents step.

3. Choosing the Data Connection. In the Choose Your Data Connection step, click New... to display the Connection Properties dialog (Fig. 22.13). (If

![](img/57baed2319be0bb1b5f98674846f2711_944_1.png)

Fig. 22.13 | Connection Properties dialog.

## 22.5 Querying a Database with LINQ

The IDE displays a Choose Data Source dialog, select Microsoft Server Database File and click Continue.) For the Data source field, if Microsoft Server Database File (SqlClient) is not displayed, click Change..., select Microsoft Server Database File (SqlClient) and click OK. Next, click Browse... to the right of the Database file name to locate and select the Books.mdf in the Directories included with this chapter. You can Test whether the IDE can connect to the database through SQL Server. Click OK to create the connection. 22.14 shows the Connection string for Books.mdf database. This contains the information that the ADO.NET Entity Framework requires to connect to the information at runtime. Click Next > A dialog will appear if you like to add the database file to your project. Click Yes to move to the next step. 

![](img/57baed2319be0bb1b5f98674846f2711_945_0.png)

22.14 | Choose Your Data Connection after selecting Books.mdf.

- 4. Choosing the Entity Framework Version. In the Choose Your Version step, the Entity Framework 6.x (Fig. 22.15), then click Next. This adds the latest version of the Entity Framework to your project.

- 5. Choosing the Database Objects to Include in the Model. In the Choose Your Database Objects and Settings step, you will specify which parts of the database that should be used in the ADO.NET Entity Data Model. Select the Tables node as shown in Fig. 22.16, then click Finish. At this point, the IDE will download the Entity Framework 6.x templates you need and add them to your project. You may see one or more Security Warning dialogs—Visual Studio displays these when you attempt to download content in your projects. Click OK to dismiss each dialog. Warnings are intended primarily for cases in which a Visual Studio template is downloaded from an untrusted website.

![](img/57baed2319be0bb1b5f98674846f2711_946_0.png)

**Fig. 22.15** | Choosing the Entity Framework version to use in the project.

![](img/57baed2319be0bb1b5f98674846f2711_946_1.png)

**Fig. 22.16** | Selecting the database's tables to include in the ADO.NET Entity Data Model.

- 6. **Viewing the Entity Data Model in the Model Designer.** At this point, the IDE creates the entity data model and displays a diagram (Fig. 22.17) in the model designer. The diagram contains **Author** and **Title** entities—these represent authors in the database and the properties of each. Notice that the IDE renamed the Title column of the Titles as Title1 to avoid a naming conflict with the class Title that represents a row in the table. The line between the entities indicates a relationship between authors and titles—this relationship is implemented in the Books database as the AuthorISBN. The asterisk (*) at each end of the line indicates a many-to-many relationship—each author can many titles. The Navigation Properties in the Titles connects the author to titles. Similarly, the Navigation Properties in the Title connects the title to authors.

![](img/57baed2319be0bb1b5f98674846f2711_947_0.png)

22.17 | Entity model diagram for Author and Title.

- 7. Building the Class Library. Select Build > Build to build the library. When you compile a library, the IDE creates a .dll file containing the library's components. This contains the information that the ADO.NET Entity Framework requires to connect to the information at runtime. Click Next > A dialog will appear if you like to add the database file to your project. Click Yes to move to the next step.
