# Using multiple-item selection controls

Sometimes you want the user to be able to choose more than one of the items available in a list. HTML has two controls that handle that: the listbox and the checkbox list. (See Figure 3-4.)

![](bbox=[0.258, 0.237, 0.796, 0.423])

**Figure 3-4:** Controls for multiple selections.

ASP.NET replicates these, like this:

+   * **The listbox:** This list is like a dropdownlist, except there is no expansion — you see the expanded list right away, scroll bar and all. To select more than one item, the user is usually to hold down the control or command key while clicking.
* **The checkboxlist:** This is exactly what it sounds like: a list of boxes. It looks just a radio button list, except with check boxes. You can see what I mean in Figure 3-4.

Here is the code for these. As the dropdownlist, the listitem is used to show the items. If it were databound, the listitems would not be — they would just be rendered from the data source at runtime.

```
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title></title>
</head>
<body>
<form id="form1" runat="server">
<div>
  1. Checkbox <br />
  <asp:ListBox ID="ListBox1" runat="server">
    <asp:ListItem Item 1</asp:ListItem>
    <asp:ListItem Item 2</asp:ListItem>
    <asp:ListItem Item 3</asp:ListItem>
    <asp:ListItem Item 4</asp:ListItem>
  </asp:ListBox>
  <br />
```