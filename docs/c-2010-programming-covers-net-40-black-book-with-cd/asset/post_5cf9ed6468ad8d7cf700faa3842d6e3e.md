
Now, the tables present in the northwnd database appear in the Tables node in the Server Explorer (Figure 26.23).

8. Drag and drop the Products table to the design surface of the DataClasses.dbml file. The output DataClasses.dbml is shown in Figure 26.23:

![](img/e073a4882197be4ab61103cbe0bcb394_1311_0.png)

Figure 26.23: Selecting the Product Table

9. Drag and drop the LinqDataSource control on the Web page and select the Configure Data Source option from its Smart Tag, as shown in Figure 26.24:

![](img/e073a4882197be4ab61103cbe0bcb394_1311_1.png)

Figure 26.24: Adding the LinqDataSource Control

Now, the Configure Data Source wizard appears (Figure 26.25).

10. Click the Next button in the Choose a Context Object page in the Configure Data Source wizard, as shown in Figure 26.25:

![](img/e073a4882197be4ab61103cbe0bcb394_1312_0.png)

Figure 26.25: Selecting the Context Object

Now, the Configure Data Selection page appears in the wizard (Figure 26.26).

- 11. Select the Columns of the Products table to display in the Gridview. In this application we have selected ProductID, ProductName, QuantityPerUnit, UnitPrice, and UnitsInStock (Figure 26.26).
- 12. Click the Finish button, as shown in Figure 26.26:

![](img/e073a4882197be4ab61103cbe0bcb394_1312_1.png)

Figure 26.26: Selecting the Columns of the Table

- 13. Build the application by selecting Build Solution option from the Build main menu.
- 14. Drag and drop the GridView control on the Design view of the Default.aspx page (Figure 26.27).

## Chapter 26: Data Binding in ASP.NET Applications

15. Select the LinqDataSource1 option from the Choose Data Source drop-down list in the GridView Tasks, shown in Figure 26.27:

![](img/e073a4882197be4ab61103cbe0bcb394_1313_0.png)

Figure 26.27: Selecting the Data Source

After configuring the data source, the Default.aspx page for the LinqDataSource application is shown in Listing 26.3:

### Listing 26.3: Showing the Code of the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:LinqDataSource ID="LinqDataSource1" runat="server" ContextTypeName="DataClassesDataContext" EntityTypeName="" Select="new (ProductID, ProductName, QuantityPerUnit, UnitPrice, TableName=\"Products\")">
            </asp:LinqDataSource>
        </div>
        <asp:GridView ID="GridView1" runat="server" DataSourceID="LinqDataSource1" AutoGenerateColumns="False">
            <Columns>
                <asp:BoundField DataField="ProductID" HeaderText="ProductID" ReadOnly="True" SortExpression="ProductID" />
                <asp:BoundField DataField="ProductName" HeaderText="ProductName" ReadOnly="True" SortExpression="ProductName" />
                <asp:BoundField DataField="QuantityPerUnit" HeaderText="QuantityPerUnit" ReadOnly="True" SortExpression="QuantityPerUnit" />
                <asp:BoundField DataField="UnitPrice" HeaderText="UnitPrice" ReadOnly="True"
```
```
SortExpression="UnitPrice" />
<asp:BoundField DataField="UnitsInStock" HeaderText="UnitsInStock" Readonly="True" SortExpression="UnitsInStock" />
</Columns>
</asp:GridView>
</form>
</body>
</html>
```

16. Press the F5 key on the keyboard to run the application. The output is as shown in Figure 26.28:

![](img/e073a4882197be4ab61103cbe0bcb394_1314_0.png)

Figure 26.28: Displaying the Output

### Using the ObjectDataSource Control

Now, let’s understand how to use the ObjectDataSource control by performing the following steps:

- 1. Create a Web application and save it as ObjectDataSource (available on the CD).
- 2. Add a Class File to the project and replace the code of the ClassProduct.cs file with the code shown in Listing 26.4:

### Listing 26.4: Showing the Code for the Class File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data;
using System.Data.SqlClient;
/// <summary>
/// Summary description for ClassProduct
/// </summary>
public class ClassProduct
{
    public DataSet getinfo()
    {
        SqlConnection con = new SqlConnection ("Data Source=PUNEET-PC\SQLEXPRESS;Initial Catalog=northwnd;Integrated Security=True");
        SqlDataAdapter da = new SqlDataAdapter ("Select * from Products", con);
        DataSet ds = new DataSet();
```

Now, the Define Data Methods page appears in the Configure Data Source wizard (Figure 26.31).

6. Select the method name from the Choose a method drop-down list and click the Finish button, as shown in Figure 26.31:

![](img/e073a4882197be4ab61103cbe0bcb394_1316_0.png)

Figure 26.31: Selecting the Method

7. Drag and Drop the GridView control on the Design view of the Default.aspx page (Figure 26.32).

8. Select the ObjectDataSource1 from the Choose Data Source drop-down list, as shown in Figure 26.32:

![](img/e073a4882197be4ab61103cbe0bcb394_1316_1.png)

Figure 26.32: Selecting the Data Source

After configuring the data source, the `Default.aspx` page for the `ObjectDataSource` application is shown in Listing 26.5:

### Listing 26.5: Showing the Code of the Default.aspx Page

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
            SelectMethod="getinfo" TypeName="ClassProduct"></asp:ObjectDataSource>
        <div>
        </div>
        <asp:GridView ID="GridView1" runat="server" DataSourceID="ObjectDataSource1">
        </asp:GridView>
    </form>
</body>
</html>
```
```

9. Press the F5 key on the keyboard to run the application. The output is as shown in Figure 26.33:

![](img/e073a4882197be4ab61103cbe0bcb394_1317_0.png)

Figure 26.33: Displaying the Output

### Using the XmlDataSource Control

Now, let’s understand how to use the `XmlDataSource` control to bind the data with the `GridView` control by performing the following steps:

- 1. Create a Web application and save it as `XmlDataSource` (available on the CD).
- 2. Add an Xml file in the App_Data folder in the Solution Explorer. Add the code in the XMLFile.xml file with the following code:

```
```xml
<student>
    <student Name="John" RollNo="A001" Standard="X"/>
    <student Name="David" RollNo="A002" Standard="XI"/>
    <student Name="Lisa" RollNo="A003" Standard="XII"/>
</student>
```
```

3. Drag and drop the XmlDataSource control and click the Smart Tag (Figure 26.34).
4. Click the Smart Tag and select the Configure Data Source option, as shown in Figure 26.34:

![](img/e073a4882197be4ab61103cbe0bcb394_1318_0.png)

Figure 26.34: Configuring the Data Source

Now, the Configure Data Source wizard appears (Figure 26.35).

5. Click the Browse button to add the XML file, as shown in Figure 26.35:

![](img/e073a4882197be4ab61103cbe0bcb394_1318_1.png)

Figure 26.35: Browsing the Data Source

Now, the Select XML File dialog box appears (Figure 26.36).

6. Select the XMLFile.xml file from the Contents of folder pane and click the OK button, as shown in Figure 26.36:

![](img/e073a4882197be4ab61103cbe0bcb394_1319_0.png)

Figure 26.36: Selecting the XML File

Now, the path of the XML file appears in the Data file text box (Figure 26.37).

7. Click the OK button in the Configure Data Source wizard, as shown in Figure 26.37:

![](img/e073a4882197be4ab61103cbe0bcb394_1319_1.png)

Figure 26.37: Saving the Path of XML File

8. Drag and Drop the GridView control on the Design view of the Default.aspx page (Figure 26.38).

9. Select the XmlDataSource1 from the Choose Data Source drop-down list, as shown in Figure 26.38:
