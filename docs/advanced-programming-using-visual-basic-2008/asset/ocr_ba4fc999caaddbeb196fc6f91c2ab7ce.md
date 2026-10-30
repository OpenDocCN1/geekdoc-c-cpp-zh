# Multiple Tiers

Now that you have worked with a DataSet object, a TableAdapter, and SQL, it's time to separate the project into multiple tiers. When possible, you should separate the database access from the user interface. For a multier application, we will create a data component as a separate tier. The data component will contain the DataSet and its TableAdapter, as well as methods to return the data to the presentation tier (Figure 3.28). When you have a well-constructed data tier, you can use the component in multiple projects with various user interfaces.

Until now you have used the VS visual designers to create the objects for database access. The visual designers automatically create all of the necessary code when you drag objects to a form. In this section, you will learn to declare and instantiate DataSet and TableAdapter objects and also to bind database objects to form controls in code.

You will find that most professional applications perform database access in code rather than use the visual designers. And when you create a separate class for database access, you must write code for binding the controls.

# Creating a Data-Tier Component

To create a data-tier component, you will add a new class to a project and write code to create and fill a DataSet. You also will need at least one method to allow the form to retrieve the DataSet. In later chapters, you will add methods for updating the DataSet.

For a Windows application, you will begin a new application and add a new data source, using the Data Sources window. This step creates the schema classes for a DataSet and TableAdapter but does not create the actual DataSet or TableAdapter objects. (In earlier projects, the DataSet and TableAdapter objects were created when you dragged data to the form.)

After you have declared the DataSet as a data source, you can write code in your new class to declare, instantiate, fill, and return the DataSet. Take a look at the code before looking at the explanation in the section that follows.

![](bbox=[0.12, 0.75, 0.68, 0.92])

# Figure 3.28

> Good applications generally separate the user interface from the data access.

# The Code

```
Public Class PubsEmployeeData
' Declare class-level variables.
Private AnEmployeeTableAdapter As PubsDataSetTableAdapters.employeeTableAdapter
```