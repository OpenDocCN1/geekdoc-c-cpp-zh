
```csharp
if (meetingDate.DayOfWeek.ToString() == "Sunday")
{
    meetingDate = meetingDate.AddDays(1);
}
```

After checking the day, the displayed calendar is changed to reflect the value stored with the meetingDate object and a message is displayed on a Label object. It contains the date and time of the meeting. This is shown in Figure 15-25.

## CUSTOMIZING THE CALENDAR AT DESIGN TIME

You can customize the display of the Calendar control object by turning on gridlines; adding borders; changing the overall size, font, background and foreground colors; or by setting the cell padding and spacing properties. Cell padding sets the amount of space between the cells and the border. Cell spacing sets the space between the cells.

## GridView Control

You were introduced to the DataGridView control in Chapter 14. This control was very useful for displaying data on a Windows form. Another data-bound control that you will want to explore is the GridView. The GridView is very similar to the DataGridView you used with Windows applications. It also features automatic data. Both the DataGridView and the GridView are used to display data in a tabular form, with each column representing a field and each row representing a record from a data source. The DataGridView, used with Windows applications, is just a little more sophisticated than the GridView control. You can customize the GridView’s appearance. As you learned in Chapter 14, when you used the DataGridView control, you must bind these types of controls to a data source.

## DATA BINDING

At design time, you can use the visual configuration tools to bind the data by identifying the data source, selecting the data fields, and setting properties in the Properties window, such as the DataSource property. Another option is to write program statements to do this. Two common data source classes used to bind GridView objects to the actual data are the DataReader and DataSet classes. The actual data used to populate these controls can come from sources such as arrays or database tables. You experienced using both the DataReader object and the DataSet object in conjunction with the DataAdapter object in Chapter 14.

> **NOTE** You are encouraged to review the sections in Chapter 14 that relate to accessing data from database tables. You will recall, from Chapter 14, that there are a number of visual tools and wizards that can be used to bind data to controls.

## USING A GRIDVIEW CONTROL IN APPLICATIONS

The WebControls application that is being developed in this chapter includes a GridView control, which displays data from an Access database. To add this control to a Web form, you follow the same design guidelines presented previously. You might want to review the DataSet Example, Example 14-21, in Chapter 14. It displayed data from an Access database on a standard Windows form. Example 14-21 instantiated objects from the DataSet and DataAdapter classes. These same classes are used to retrieve data for display on a Web form in this example.

> NOTE
> You would follow the same principles to connect your Web site to a SQL database. Access was used in this chapter because it was used in Chapter 14. However, you would normally want to connect a Web site to a database that handles multiple users.

### OleDB Data Provider
You learned in Chapter 14 that .NET organizes ADO.NET classes into different provider namespaces. This enables you to work with data from different databases such as Oracle and Access using a consistent object-oriented approach. Each of these namespaces has its own classes prefixed with the provider type, one of which is OleDB for working with Access databases.

> NOTE
> Visual Studio has a Data tab as part of the Toolbox. Included are controls for displaying data such as the GridView, DataList, and DetailsView controls plus controls that are used to connect to specific databases. These include AccessDataSource, SqlDataSource, XmlDataSource, and ObjectDataSource. All of these controls can be dragged to your form in exactly the same manner you drag other control objects, such as buttons.

## CONNECTING TO THE DATABASE

A button labeled See Current Members is added to the WebControls application. When the user clicks the button, a table should be displayed with the names of current members. A solution can be developed by writing program statements to populate a control. This approach will be explored first. However, with the visual tools available with Visual Web Developer and Visual Studio, another approach will then be illustrated that minimizes the amount of program statements required. A Connection object is instantiated. The same connection string that you saw in Chapter 14 is used as an argument to the constructor. The connection string identifies the provider as an Access database. It also specifies the name of the database—including the full path to the database location. The example that follows, Example 15-14, shows the statements that make up the btnShowMembers_Click() method. As you review the code, notice the comment that appears in the method. Only minor modifications are needed to the code presented in Chapter 14. The DataBind() method call is different for Web applications. To display the data using the GridView, objects of the DataAdapter and DataSet classes are used for both Web and Windows applications.

> **NOTE**
> Note that the path of the database is listed as `"C:\\CSharpProjects\\member.accdb"`. You will want to change the path indicating where you have placed a copy of the `member.accdb`.

## EXAMPLE 15.14

```csharp
protected void btnShowMembers_Click(object sender, EventArgs e)
{
    lblMembers.Visible = true;
    try
    {
        string sConnection =
            "Provider=Microsoft.ACE.OLEDB.12.0;" +
            "Data Source=C:\\CSharpProjects\\member.accdb";
        OleDbConnection dbConn = new OleDbConnection(sConnection);
        string sql =
            "Select FirstName as [First Name], LastName as " +
            "[Last Name] From memberTable " +
            "Order By LastName Asc, FirstName Asc;";
        OleDbCommand dbCmd = new OleDbCommand();
        dbCmd.CommandText = sql;
        dbCmd.Connection = dbConn;
        OleDbDataAdapter memberDataAdap = new OleDbDataAdapter();
        memberDataAdap.SelectCommand = dbCmd;
        DataSet memberDS = new DataSet();
        memberDataAdap.Fill(memberDS, "memberTable");
        grdViewMembers.DataSource = memberDS;
        // Binding is required for web apps
        this.grdViewMembers.DataBind();
        lblMembers.Visible = true;
        grdViewMembers.Visible = true;
    }
    catch (System.Exception exc)
    {
        this.lblMsg.Text = exc.Message;
    }
}
```

> **NOTE**
> If you use the Data Source Configuration wizard to connect to the database, an `asp:AccessDataSource` control tag is added to the .aspx file. One of its attributes is `DataFile="~/App_Data/member.accdb"`.

## RETRIEVING DATA FROM THE DATABASE
Example 14–21 in Chapter 14 contained statements that created a Windows application with a DataGridView object populated from the Member.accdb database. Example 15–14 is similar but stores the retrieved data on a Web Form. As with Example 14–21, a SQL statement stored in the string identifier, sql, is used to select the records. In this example, the data fields of FirstName and LastName from memberTable are retrieved. The SQL statement arranges the result by LastName. When there are duplicate records with the same last name, the records are arranged in ascending order by FirstName. In order to programmatically change the column heading for the GridView, the as keyword was used. Square brackets were used around the identifier to enable a space to be included as part of the name. Writing Select FirstName as [First Name], retrieves the data field named FirstName and uses "First Name" as the column heading. The sql string object is set as the CommandText property value. The connection string, dbConn, is set as the Connection property as follows:

```
dbCmd.CommandText = sql;
dbCmd.Connection = dbConn;
```

To use the Fill() method with the DataSet object, an object of the DataAdapter class is instantiated. Notice that each of these classes is part of the OleDb namespace, thus class names are prefixed with OleDb. Additional using statements were added to include the Data and Data.OleDb namespaces. The SelectCommand property of the DataAdapter class is set to the CommandText object holding the SQL statement. Using the DataAdapter’s Fill() method, the table from the actual Access database (memberTable) is used to populate the DataSet object (memberDS). The final statements in the try block for Example 15–14 binds the GridView object to the DataSet. Recall that this is the only statement that changed from the Windows application.

> NOTE — Remember, Figure 15-19 shows this application running after all the controls are added to the page and event-handler methods are wired.

The complete program listing for the code-behind file for the WebControls project is shown in Example 15–15.

## EXAMPLE 15.15

```csharp
// WebControls
using System;
using System.Collections.Generic;
using System.Linq;
using System.Data;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data.OleDb;
```
