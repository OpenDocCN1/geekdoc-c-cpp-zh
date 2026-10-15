# Using the Grouping Operator

You can use the group query results based on some key value. The GroupBy clause is used to group the query in LINQ based on a common key. Now, let’s create an application in which you can group your query using the GroupBy clause. Create a website and save it as GroupClause (available on the CD).

To add the required controls, you can find the code for the Default.aspx page in Listing 27.20:

# Listing 27.20: Showing the Code for the Default.aspx Page

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
<title>Using Group Clause</title>
</head>
<body>
<form id="form1" runat="server">
<div id="header">
<h1>
C# 2010 Black Book
</h1>
</div>
<div id="content">
<div class ="itemContent">
<br />
<br />
Displays data by using GroupBy clause<br />
&nbsp;<br />
&nbsp;<asp:ListBox ID="ListBox1" runat="server" Height="150px" style="margin-left: 120px" Width="295px"></asp:ListBox>
<br />
<br />
<asp:Button ID="Button1" runat="server" onclick="Button1_Click" style="margin-left: 152px" Text="Display" Width="105px" />
<br />
</div>
</div>
</form>
</body>
</html>
```

After modifying the code in the source file, change the code in the code-behind file of the Default.aspx page, as shown in Listing 27.21:

# Listing 27.21: Showing the Code for the Code-Behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
```