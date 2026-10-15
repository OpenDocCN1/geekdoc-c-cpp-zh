![](bbox=[0.105, 0.069, 0.91, 0.463])

After adding the table to the MyClasses.dbml file, add the code for the Default.aspx page as shown in Listing 27.1:

# Listing 27.1: Showing the Code for the Default.aspx Page

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="default.aspx.cs"
    Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
    <title>LINQ to SQL Example</title>
</head>
<body>
    <form id="form1" runat="server">
        <div id="header">
            <h1>
                C# 2010 Black book
            </h1>
        </div>
        <div id="content">
            <div class="itemContent">
                <asp:ListBox ID="ListBox1" runat="server" Height="292px" Width="431px"
                    style="margin-left: 78px; margin-top: 32px"></asp:ListBox>
            </div>
        </div>
    </form>
</body>
</html>
```
```