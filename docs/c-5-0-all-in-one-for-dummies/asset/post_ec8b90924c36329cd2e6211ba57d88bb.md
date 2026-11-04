
You can pick a web service to connect to a function on another computer. I cover web service creation and consumption in Book V, but this functionality sets you up to have a data source along with the web service reference. It's cool. An example of the blank screen is shown in Figure 2-3.

![](img/80ff26f06fc9ab951e1cd4257b867366_449_0.png)

When you finish looking around, click the Cancel button to return.

- **5. Click the Database data source type to be taken to the Choose a Database Model screen.**

For this example, I just used an Entity Data Model. The next part of the wizard is the Entity Data Model Wizard, as shown in Figure 2-4. You want to select Generate from Database.

- **6. If you have an existing data connection, it appears in the drop-down list; otherwise, you need to click the New Connection button to bring up the Add Connection dialog box, shown in Figure 2-5.**

For this example, I click the New Connection button and select Microsoft SQL Server Database File.

![](img/80ff26f06fc9ab951e1cd4257b867366_450_0.png)

**Figure 2-4:**  
Choosing your data connection.

![](img/80ff26f06fc9ab951e1cd4257b867366_450_1.png)

**Figure 2-5:**  
The Add Connection dialog box.

The Add Connection dialog box assumes that you’re going to connect to a SQL server. If that isn’t the case, click the Change button to select a different database from the Change Data Source dialog box, as shown in Figure 2-6. For this example, I chose Microsoft SQL Server Database File and clicked OK.

Depending on what edition of SQL Server you have installed, you may see extra steps. You may be asked by Visual Studio to upgrade the database file, which is totally fine. If you're in a large-scale enterprise environment, check with your database administrator as to the best way to connect to your database system.

![](img/80ff26f06fc9ab951e1cd4257b867366_451_0.png)

Figure 2-6:
The Change Data Source dialog box.

If you do use a database file, Visual Studio will copy pertinent files to your project. If you're working through this book in an isolated project, that's fine. If you're on a development effort with others, check to make sure that it's appropriate to your life cycle methodology.

- **7. Click the Next button to save the connection string to the application configuration file.**
- **8. Accept the defaults by clicking Next.**
- You see the Choose Your Database Objects and Settings screen. You can choose the tables, views, or stored procedures that you want to use.
- **9. Under Tables, select Product and ProductCategory (under the Production heading, as shown in Figure 2-7), and click Finish.**

You're done! If you look at the designer, you can see that an Entity Data Model was added to your project with the two tables on the design surface, as shown in Figure 2-8.

![](img/80ff26f06fc9ab951e1cd4257b867366_452_0.png)

**Figure 2-7:** Selecting data objects.

![](img/80ff26f06fc9ab951e1cd4257b867366_452_1.png)

**Figure 2-8:** New data connections appear in the Data Sources panel to the left.

## Book III
Chapter 2
Accessing Data

By following the preceding steps, you create two significant entities in Visual Studio:

- You create a connection to the database, shown in the Server Explorer. You find that it sticks around — it’s specific to this installation of Visual Studio.
- You also create an Entity Data Model, which is specific to this project and won’t be there if you start another project.

Both of them are important, and they provide different functionality. In this chapter, I focus on the project-specific data source displayed in the Entity Data Model.

## Working with the visual tools

The Rapid Application Development (RAD) data tools for C# are a massive improvement over what Microsoft previously provided. The RAD data tools in Visual Studio are usable and do what you need, and they write decent code for you.

![](img/80ff26f06fc9ab951e1cd4257b867366_453_0.png)

You need to know that I would never show this kind of black magic if it weren’t a best practice. In the past, tools that did something you couldn’t see often did their job poorly. Using the tools, in the long run, made your program worse. The new tools, though, are a good way to build software. People may tell you that I am wrong, but it really isn’t bad. Try it!

If you select the Data Sources panel (View⋗Other Windows⋗Data Sources) and click a table in the panel, a drop-down arrow appears, as shown in Figure 2-9. Click it, and you see something interesting: A drop-down list appears, and you can then choose how that table is integrated into Windows Forms.

Change the Product table to Details View. It’s used to create a detail type form — one that easily enables users to view and change data. Then drag the table to the form, and Details View is created for you, as shown in Figure 2-10.

A whole lot of things happened when you dropped the table on your form:

- The fields and the field names were added.
- The fields are in the most appropriate format.
- The field name is a label.
- Visual Studio automatically adds a space where the case changes.

![](img/80ff26f06fc9ab951e1cd4257b867366_454_0.png)

**Figure 2-9:** Table Options drop-down list.

![](img/80ff26f06fc9ab951e1cd4257b867366_454_1.png)

**Figure 2-10:** Creating a Parts Detail data form.

![](img/80ff26f06fc9ab951e1cd4257b867366_455_0.png)

Note that each field gets a SmartTag that enables you to specify a query for the values in the text box. You can also preset the control that's used by changing the values in the Data Sources panel (refer to Figure 2-10).

Also, a VCR Bar (technically called the BindingNavigator) is added to the top of the page. When you run the application, you can use the VCR Bar to cycle among the records in the table.

Finally, four completely code-based objects are added in the Component Tray at the bottom of the page: the DataSet, the BindingSource, the DataAdapter, and the BindingNavigator objects.

Click the Play button, and you can see the VCR Bar work. You can walk through the items in the database with no problems, as shown in Figure 2-11. It’s just like working in Access or FoxPro, but with enterprise quality!

## Writing data code

In most enterprise development environments, however, you won’t be using the visual tools to build data access software. Generally, an infrastructure is already in place.

The reason for this is that often, enterprise software has specific requirements, and the easiest way to manage those specifications is with unique and customized code. In short, some organizations don’t want things done the way Microsoft does them.

![](img/80ff26f06fc9ab951e1cd4257b867366_455_1.png)

## Output of the visual tools

The reason that the visual tools often aren't used in enterprise environments is that the code the tools put out is rather sophisticated. If you switch to Code View and right-click an instance of an object (such as the PartsTableAdapter object) and select Go to Definition, you see the code behind the designer.

Figure 2-12 shows what you see when you first get in there. The box marking the region near the top of the code window is marked as Windows Form Designer generated code, and you can't help but notice that the line number before that section is in the twenties and the number after that is in the four hundreds. That's a lot of generated code.

![](img/80ff26f06fc9ab951e1cd4257b867366_456_0.png)

Figure 2-12: Generated code. Huh?

Nothing is wrong with this code, but it is purposely generic to support anything that anyone might want to do with it. Enterprise customers often want to make sure that everything is done the same way. For this reason, they often define a specific data code format and expect their software developers to use that, rather than the visual tools.

## Basic data code

The code of the sample project is simple:

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
```
