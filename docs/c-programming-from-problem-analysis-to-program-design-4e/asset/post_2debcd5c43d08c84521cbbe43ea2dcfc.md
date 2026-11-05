
The database that was last accessed is automatically, by default, established. If you want to use a different database, you would **Add New Data Source**. If you want to use that same connection, nothing else is required.

> **NOTE**
> Another option for making a local copy of the database for your project is to use **Windows Explorer** and drag a copy of the database to the **Visual Studio Solution Explorer** window. The copy should be dropped on top of the project node. When you do this, the **Data Source Configuration Wizard** launches and gives you an opportunity to identify which table(s) to include in the dataset. **Access database files end with an .accdb extension.** SQL Express database files end with an .mdf extension.

Both Microsoft Access and SQL Server databases can be stored locally with your project. If multiple applications are using the same database, you will probably prefer to leave the database in its original location so that changes made by one application are available to all other applications using the database. Thus you would probably select **No** when prompted as shown in Figure 14-11.

> **NOTE**
> If you are using the **Data Source Configuration** and **DataSet Designer** tools and are planning to update or make changes to the database within your application, it is recommended that you not make a local copy of the database. The underlying database does not get changed properly. Having a local copy works fine if you only intend to display the data.

## CONNECTION STRING CREATED

Visual Studio offers to store the connection string in a configuration file that contains settings specific to your application. This is illustrated in Figure 14-12. As a final step before you identify the data to be placed in the dataset, you decide whether to store the connection string.

![](img/36e48639a06772bcb0fa1ea2525b33a3_969_0.png)

**FIGURE 14-12** Save connection string

As shown in Figure 14-12, storing the connection string in the application’s configuration file makes maintenance and deployment easier. It simplifies the process of maintaining your application if the database connection changes. In the event of a change in the database connection, you can edit the connection string in the application configuration file as opposed to editing the source code and having to recompile your application. The default name for the connection string for the application is the name of the database followed by ConnectionString; thus for this example the name is StudentDataBaseConnectionString, as shown in Figure 14-12.

If you save the connection string to the application configuration file, as shown in Figure 14-12, an App.config file is created. Example 14-22 shows the file contents. It is an XML file that can be viewed and modified in Visual Studio.

### EXAMPLE 14.22

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
  </configSections>
  <connectionStrings>
    <add name="ConfigToolsExample.Properties.Settings.StudentDataBaseConnectionString" connectionString="Provider=Microsoft.ACE.OLEDB.12.0; Data Source=|DataDirectory|\StudentDataBase.accdb" providerName="System.Data.OleDb" />
  </connectionStrings>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework, Version=v4.5" />
  </startup>
</configuration>
```

If you look ahead at Figure 14-14, you will find the App.config file listed in the **Solution Explorer** window for the project.

## Dataset Object

As a final step in using the configuration tool, you identify the database objects that you want to bring into your application. As shown in Figure 14-13, a tree-like structure shows the views, tables, and columns available from the data source you selected.

![](img/36e48639a06772bcb0fa1ea2525b33a3_971_0.png)

**FIGURE 14-13** Choose dataset objects

The chosen objects and their underlying data are brought into your application and become accessible through the dataset object. You can select to include in your dataset all of the tables and/or views of the database. You also have the option of selectively identifying individual tables, as shown in Figure 14-13. Another option is to select certain columns to have available in memory as your dataset object.

The dataset that is created not only includes the collection of one or more data table objects made up of rows and columns of data, but it also includes primary and foreign keys, constraints, and relation information about the data.

You will recall that dataset objects, used with data adapter objects, enable you to update the original data source. As shown in Figure 14-14 in the **Solution Explorer** window, StudentDataBaseDataSet.xsd is created.

![](img/36e48639a06772bcb0fa1ea2525b33a3_972_0.png)

**FIGURE 14-14** Data Sources and Solution Explorer windows

As highlighted in Figure 14-14, the App.config file, which stores the connection string, is now part of the application. A new set of files defining the dataset object is also included with the application when the configuration wizard terminates normally. These files, independent of the data source, are also named using the database identifier (e.g., StudentDataBaseDataSet.xsd) with "DataSet" appended onto the end of the name.

## DATA SOURCES WINDOW

Figure 14-14 also shows the new Data Sources window to the left of the form. This window enables you to view the data available to your project. It greatly reduces the complexity of binding data from a database to controls on your forms by allowing you to drag complete tables or selectively drag columns from the tables onto forms to create data-bound controls.

Data was placed in rows and columns in an earlier example using the DataGridView.

The DataGridView has additional functionality not used in the previous example. You can specify how data is formatted and displayed using the DataGridView. It provides a customizable table that allows you to modify columns, rows, and borders. You can freeze rows and columns to prevent them from scrolling. You can hide rows or columns and provide ToolTips and shortcut menus for individual cells, rows, and columns in the grid.

## PLACING A DATAGRIDVIEW CONTROL ON THE FORM

The easiest way to add a DataGridView control to your application is to drag a table from the Data Sources window onto your form. When you do this, an object of the DataGridView class is instantiated. You get the added benefit of another control, a BindingNavigator object, being automatically instantiated. In Figure 14-15, notice the strip of buttons below the title bar. These were all placed when the table from the Data Sources window was dragged onto your form; no additional coding was needed. No other objects (other than the DataGridView) were dragged onto the form.

![](img/36e48639a06772bcb0fa1ea2525b33a3_973_0.png)

**FIGURE 14-15** DataGridView control placed on form

As shown in Figure 14-15, in addition to the grid-like control being placed on the form along with the navigational strip, five objects are placed in the Component Tray. These objects will all be explored after you take a closer look at the DataGridView object.

## CUSTOMIZING THE DATAGRIDVIEW OBJECT

One way to customize the DataGridView control is to use its smart tag. You will recall that the smart tag glyphs are displayed when you select the control. They float at the upper-right corner above the control. The DataGridView tasks are shown in Figure 14-16.

![](img/36e48639a06772bcb0fa1ea2525b33a3_974_0.png)

**FIGURE 14-16** Customizing the DataGridView control

The DataGridView control has many properties that can be set through the **Properties** window. Clicking the control's smart tag reveals several other customization tool options. Selecting **Dock in Parent Container** causes the grid to expand to the form size. This is especially useful if only one control will be displayed on the form. As you experiment with the settings, notice that this menu option toggles to become **Undock in Parent Container** after it is selected.

## EDITING COLUMNS

From the **DataGridView**'s smart tag, the **Edit Columns** option displays the columns, allowing you to remove or reorder them. Initially they appear in the same order and by the same name as the columns in the dataset. Recall that the dataset is generated from the table, so the column names are field names in the database. When you click the **Edit Columns** option, you'll see the **Bound Column Properties** for each of the columns. The **Bound Column Properties** option, shown in Figure 14-17, is similar to the **Properties** window but is used to set values specifically for the column objects being displayed on the **DataGridView** control.
