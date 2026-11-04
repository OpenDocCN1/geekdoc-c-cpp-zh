![](bbox=[0.22, 0.13, 0.85, 0.62])

Figure 3-2:
The three text inputs, all in a row.

+   - **TextMode:** This determines the type of text box that gets rendered, as I mentioned.
+   - **MaxLength:** The maximum number of characters that the user can type in the field. Note that this doesn't work when the TextMode is defined as TextArea.
+   - **Height and Width:** The size that the text box appears on the page.
+   - **CssClass:** The style sheet class that the control will be rendered to use. Must be used in conjunction with a style sheet.
+   - **Enabled:** Marks if the field can be typed in by the user.

In the example in Figure 3-1, I just dragged the TextBox control onto the designer three times and set each to the three different TextModes. Here is the resultant ASP.NET markup:

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="TextInput.aspx.cs"
    Inherits="Chapter_3_WebForm1" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.
W3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
```