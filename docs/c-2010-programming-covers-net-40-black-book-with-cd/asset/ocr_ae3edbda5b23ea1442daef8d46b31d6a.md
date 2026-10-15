After configuring the data source, the `Default.aspx` page for the `ObjectDataSource` application is shown in Listing 26.5:

# Listing 26.5: Showing the Code of the Default.aspx Page

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

![](bbox=[0.272, 0.394, 0.779, 0.719])

# Figure 26.33: Displaying the Output

# Using the XmlDataSource Control

Now, let’s understand how to use the `XmlDataSource` control to bind the data with the `GridView` control by performing the following steps:

+   1. Create a Web application and save it as `XmlDataSource` (available on the CD).
+   2. Add an Xml file in the App_Data folder in the Solution Explorer. Add the code in the XMLFile.xml file with the following code:

```
```xml
<student>
    <student Name="John" RollNo="A001" Standard="X"/>
    <student Name="David" RollNo="A002" Standard="XI"/>
    <student Name="Lisa" RollNo="A003" Standard="XII"/>
</student>
```
```