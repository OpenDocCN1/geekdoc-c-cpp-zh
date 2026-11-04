This isn't the interesting way to bind things. It is nice because you can edit the binding without recompiling but the interesting way is in the C# code. Doing it in the C# code is much more readable and manageable. There are times to use each, but this is a C# book. The least we can do is to focus on the code-behind, right?

# Data binding using the code-behind

Rather than set a property directly in the markup, we can set it equal to a value in the code-behind. For a repeating control, we can set a DataSource property in the C# code for the control. Then, when we bind the page, it uses that value to load in the right value or values from the code-behind.

Keep in mind, though, that with the Text property of a Label (for instance) this just simple data binding. I am just setting a value.

Let's try it with the earlier example. Just follow these steps:

1. Keep the label text simple — just drop the Text property, like this:

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Text.aspx.cs" Inherits="Chapter_3.Text" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" >
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
This is some text.<br />
<asp:Label ID="Label1" runat="server" />
</div>
</form>
</body>
</html>
```

2. In the code-behind, set the Text property equal to the property on the control that you want to bind to.

Notice that there is no DataBind command for the page:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
```