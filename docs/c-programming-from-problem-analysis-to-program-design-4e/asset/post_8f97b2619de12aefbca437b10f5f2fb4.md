
Connection string property; you just identify the location of the Access .accdb file, as shown in Figure 15-29.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1081_0.png)

**FIGURE 15-28** Database file stored in App_Data directory

If the Access database is in the App_Data directory, you browse to that location and a relative path is set, as shown in Figure 15-29.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1082_0.png)

**FIGURE 15-29** Relative address for the Access database

> **NOTE**
> You can place your database in the App_Data directory using the Solution Explorer window by right-clicking on the App_Data folder and selecting Add, Add Existing Item. You can then Browse to its original location.

The database is now referenced by a relative path (for example, ~/App_Data/member.accdb). If you move the Web site, ASP.NET will look for the database in the App_Data folder of the application. This is one of the advantages of using the configuration tools. It is no longer necessary for you to locate and change the path for the database in your source code if the Web site gets moved.

After the file is located, the Configure Data Source wizard enables you to identify which table(s) and field(s) to display on the GridView. This is shown in Figure 15-30.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1083_0.png)

**FIGURE 15-30** Identify what data to retrieve

As shown in Figure 15-30, the database table(s) are selected from a dropdown list. The query builder tool is launched if you select the **WHERE** button. To have the items displayed in ascending or descending order by a specific field, the **Order By** option is used. For the WebControls application, the records were ordered by LastName and then by FirstName. As shown at the bottom of the display in Figure 15-30, a SQL select statement is generated based on your selections. The **Test Query** button enables you to see what will be returned from the query.

Options are available from the GridView's smart tag after you complete the data source configuration. The list of **GridView Tasks** is shown in Figure 15-31.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1084_0.png)

**FIGURE 15-31** GridView tasks

As shown in Figure 15-31, you now have options to enable paging, sorting, and selection. Selecting the **Enable Sorting** option makes it possible for you to select a column and have the table reordered by that field. If you want to change the column heading, do this using the **Edit Columns** option. The **Edit Columns** option displays a dialog box where each field's properties can be changed. A number of properties are available for each field grouped by Accessibility, Appearance, Behavior, Data, and Style. The **Header Text** was set for both columns and the **BackColor** property for the **HeaderStyle** for both the last and first names was set to yellow (#FFFFC0). The **FirstName** column was moved up so that it appears first.

## Setting the Visibility Property

The **btnShowMembers_Click()** method of the WebControls application with the **GridView** no longer needs code to connect to the database and populate the control on the page. Recall that this is done behind the scenes by the **Configure Data Source** wizard. If you review Examples 15-14 and 15-15, you will notice that the first line of code in the **btnShowMembers_Click()** method for Example 15-14 was a statement that made the label over the table visible when the user clicked the **See Current Members** button. The same line of code (`lblMembers.Visible = true;`) is also part of Example 15-15. If you also want to wait to display the GridView object after the user clicks this button, the Visible property should initially be set to false for both the Label and the GridView. Another line of code needs to be added to this method to make the GridView visible. The new btnShowMembers_Click() is shown in Example 15-16. All of the database connection code is deleted.

**EXAMPLE 15.16**

```
protected void btnShowMembers_Click(object sender, EventArgs e)
{
    lblMembers.Visible = true;
    grdViewMembers.Visible = true;
}
```

## MODIFYING THE DATA

By default, the GridView control displays data on a Web form in a read-only format. To allow users to edit data stored in the GridView object, you can use the **Advanced** button to configure the select statement from the **Data Source Configuration** tool. This Advanced button is shown in Figure 15-30. Selecting this option generates the additional Insert, Delete, and Update SQL statements needed.

To use this feature, all primary key values must be retrieved as part of the select statement during the data source configuration. The key fields do not have to be displayed on the GridView. They can be removed using the smart tag after the configuration is complete; however, the query must return their values.

> **NOTE** Be cautious about not including primary key results in your display. If you have specified that a key field cannot be null, you will not be able to add records if no value is entered for the key.

After the SQL statements are available for the InsertCommand, UpdateCommand, and DeleteCommand, the smart tag for the GridView reveals additional options of **Enable Editing** and **Enable Deleting**. If you select these options, an additional column is added to the GridView table, as shown in Figure 15-32.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1086_0.png)

**FIGURE 15-32** Modifying the data table

> **NOTE:** Recall from Chapter 14 that a question mark (?) is used as part of the SQL statement to indicate a parameterized value for the user to enter, and for update queries with Access databases. An ampersand (&) is used with SQL Server Express.

As shown in Figure 15-32, when the application is run, the column displays buttons labeled **Edit** and **Delete**. Clicking the **Edit** button causes the row of data to be displayed in an editable format. Because the **StudentID** is a primary key, it is not editable. Notice that on the row being modified, the **Edit** button is replaced with **Update** and **Cancel** buttons. After you change the data and click the **Update** button, the UpdateCommand event is raised or triggered, and the code written to change the data in the database table is executed.

## Other Controls

You are encouraged to review Figure 15-17. It shows the many different Web Forms controls that can be added to a Web Forms page from the **Toolbox** using a drag-and-drop approach. A number of Web Forms server controls are available to you. Explore the **System.Web.UI.WebControls** namespace to find others. Not all of the Web server controls are included in the **Toolbox**.

Because of space constraints, this chapter uses only a small subset of the classes available to you for creating ASP.NET applications. Over 250 classes make up the **System.Web.UI.WebControls** namespace.

### NAVIGATION

For navigation purposes, you can add site navigation to your Web sites by defining a site map. You do this using one of the navigation controls, such as the **TreeView** and **SiteMapPath** controls. These controls automatically create menu or tree views of pages. There are a number of classes focusing on security and navigation.

### DATA

You have a very large selection of controls for working with data. You experienced the GridView control in this chapter. You will want to explore the DetailsView and FormView controls. They are also used to display and edit data from different data sources. You saw in this chapter how the smart tag for the GridView enabled you to bind the control to a data source. The connections, queries, and parameters are all now encapsulated with these other data source controls. These data source controls automatically retrieve data when the page runs, cutting down the need to write code to execute commands and manage data scenarios.

### LOGIN

ASP.NET provides security controls that enable you to authenticate users with a suite of login controls. The Login control prompts users for credentials and validates them. The PasswordRecovery control helps users change or remember their password. The LoginStatus control lets you present a Login or Logout button.

Entire books are written on ADO.NET and ASP.NET. The intent is to give you a foundation and introduce you to what is available, so that you can continue learning after finishing this chapter. You might want to do that by exploring some of the classes listed in Table 15-4. The table was adapted from Visual Studio's MSDN documentation—retrievable using the **Help**, **Search** menu option.

**TABLE 15-4** Additional Web Forms control classes

| Class Identifier | Description |
|---|---|
| AccessDataSource | Represents a Microsoft Access database to data-bound controls |
| AdRotator | Displays an advertisement banner on a Web page |
| ChangePassword | Provides a user interface that enables users to change their Web site password |
| Content | Holds text, markup, and server controls to render to a ContentPlaceHolder control in a master page |
| ContentPlaceHolder | Defines a region for content in an ASP.NET master page |
| DataList | A data-bound list control that displays items using templates |
| DetailsView | Displays the values of a single record from a data source in a table, where each data row represents a field of the record; the DetailsView control allows you to edit, delete, and insert records |

_(continues)_
