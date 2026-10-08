
An examination of all them would not fit into this chapter. Instead of showing all the nitty-gritty details, this section focuses on getting started with these controls, and helps you to discover them on your own.

The best way to become familiar with the new server controls is to learn them through example. You can download the ActControlSamples project from this book's companion website (www.wrox.com) and try the samples introduced here.

# The ComboBox Control

The ComboBox control of the Toolkit is very similar to the ComboBox control you can use with Windows Forms. But, of course, you can use it with ASP.NET applications. It can be described as a DropDownList that typed directly into like a TextBox. The semantics of ComboBox are also very similar to ASP.Net DropList.

Open the ActControlsSample. You'll find a page named ComboBox.aspx. This page contains a DropDownList control to use the AutoCompleteMode of the other two ComboBox controls on the page. The first ComboBox instance is initialized in the .aspx file; the second picks up values from a database. When you sample it, you see the page shown in Figure 20-6.

Listing 20-8 shows the source code of the UI.

![](img/b5597c749e848b27b0d305153ae16106_957_0.png)

FIGURE 20-6: ComboBoxSample.aspx page

![](img/b5597c749e848b27b0d305153ae16106_957_1.png)

```assembly
<%@ Language="C#" AutoEventWireup="true"
CodeBehind="ComboBoxSample.aspx.cs"
Inherits="ActControlSamples.ComboBoxSample" %>

<%@ Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit"
TagPrefix="asp" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/html/html-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
runat="server">
<title>Ajax ComboBox sample</title>
</head>
<body>
<form id="form" runat="server">
<asp:ToolkitScriptManager ID="ToolkitScriptManager" runat="server" />
<div>
<p>
Select <code>AutoCompleteMode</code>; value from this
```

```html
<code></code></p>
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
<ContentTemplate>
<asp:DropDownList ID="AutoCompleteList" runat="server"
AutoPostBack="true"
OnSelectedIndexChanged="AutoCompleteList_SelectedIndexChanged">
<asp:ListItem Value="None" />
<asp:ListItem Value="Append" />
<asp:ListItem Value="Suggest" />
<asp:ListItem Value="SuggestAppend" />
</asp:DropDownList>
<p>
 Simple <code>ComboBox&gt; filled with numbers:/&gt;</p>
<asp:ComboBox ID="SimpleComboBox" runat="server"
AutoPostBack="true"
OnSelectedIndexChanged="SimpleComboBox_SelectedIndexChanged"
OnItemInserting="SimpleComboBox_ItemInserting">
<asp:ListItem Value="0">Please select a value</asp:ListItem>
<asp:ListItem Value="1">One</asp:ListItem>
<asp:ListItem Value="2">Two</asp:ListItem>
<asp:ListItem Value="3">Three</asp:ListItem>
<asp:ListItem Value="4">Four</asp:ListItem>
</asp:ComboBox>
&nbsp;
<asp:Label ID="SimpleComboBoxLabel" runat="server" Text="" />
</ContentTemplate>
</asp:UpdatePanel>
<p>
<code>ComboBox&gt; filled from a database:/&gt;</p>
<asp:ComboBox ID="DataComboBox" runat="server"
AutoPostBack="true"
OnSelectedIndexChanged="DataComboBox_SelectedIndexChanged"
DataSourceID="ExpertDataSource"
DataField="Name"
DataValueField="ID"
MaxLength="0"
<asp:AccessDataSource ID="ExpertDataSource" runat="server"
DataFile="/App_Data/ExpertData.mdb"
SelectCommand="SELECT * FROM [Expertise]"
</asp:AccessDataSource> &nbsp;
<asp:Label ID="DataComboBoxLabel" runat="server" Text="" /> <br />
</div>
</form>
</body>
</html>
```

![](img/b5597c749e848b27b0d305153ae16106_958_0.png)

You can encapsulate the ComboBox controls into an UpdatePanel. However, it is not required to make them. Use that the SimpleComboBox is wrapped in an UpdatePanel, while

DataBoundComboBox is not. The two ComboBox instances raise a few events that let you examine how they work. By both of them respond to the SelectedChanged event, and display the current selection. Listing 20-9 shows the code behind the UI.

# LISTING 20-9: ComboBoxSample.ascx

```csharp
using System;
using System.Data;
using System.Data.OleDb;
using System.Web.UI.WebControls;
using AjaxControlToolkit;

namespace ActControlSamples
{
public partial class ComboBoxSample : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    }

    protected void AutoCompleteList_SelectedIndexChanged(object sender, EventArgs e)
    {
        var autoComplete = (AutoCompleteMode)Enum.Parse(typeof(AutoCompleteMode), AutoCompleteList.Value);
        SimpleComboBox.AutoCompleteMode = autoComplete;
        DataBoundComboBox.AutoCompleteMode = autoComplete;
    }

    protected void SimpleLabel_SelectedIndexChanged(object sender, EventArgs e)
    {
        SimpleLabel.Text = String.Format("{0}: {1}", SimpleComboBox.Value, SimpleComboBox.SelectedItem);
    }

    protected void ComboBoxItem_ItemInserted(object sender, EventArgs e)
    {
        SimpleLabel.Text = String.Format("{0}: {1}", SimpleComboBox.Value, SimpleComboBox.SelectedItem);
    }

    protected void SimpleComboBox_ItemInserting(object sender, ComboBoxItemEventArgs e)
    {
        if (e.Item.Text.StartsWith("Q"))
        {
            e.Cancel = true;
            return;
        }
    }
}
```csharp
if (e.Item.Text.StartsWith("E"))
  e.InsertLocation = ComboBoxInsertLocation.Ordinal;
else if (e.Item.Text.StartsWith("N"))
{
  e.InsertLocation = ComboBoxInsertLocation.Append;
  e.Value = SimpleComboBox.Items.Count.ToString();
}
```csharp
protected void DataBoundCombo_SelectedIndexChanged(object sender, EventArgs e)
{
  DataBoundComboLabel.Text = String.Format("{0}: {1}", DataBoundCombo.Value, DataBoundCombo.SelectedItem);
}
```

Code file ComboBoxSample.aspx available for download at Wrox. The AutoComplete allows you to select the value of the AutoCompleteMode property. This determines how the ComboBox automatically completes the text that you type:

- When Suggested is specified, the ComboBox will show the list, highlight the first matched item, and if necessary, scroll the list to show the highlighted item.
- When Append is specified, the ComboBox will append the remainder of the first matched item to the user-typed text, and highlight it.
- When SuggestAppend is specified, both of these behaviors are applied.
- When None (the default value) is specified, the ComboBox's auto-complete behaviors are disabled.

Figure-20 shows how the SimpleComboBox behaves when SuggestAppend mode is specified.

The most interesting method in Listing 20-9 is SimpleComboBox_ItemInserting that is invoked when a text value is about to be inserted into the combo. This method cancels the insertion for any text starting with Q. By default, the new text is appended at the end of the list. But this code changes this behavior so that, when you insert a text starting with E, it will be inserted into the list according to the new text's ordinal (alphabetical) position.

![](img/b5597c749e848b27b0d305153ae16106_960_0.png)

FIGURE 20-7: ComboBox using AutoMode set to SuggestAppend

The new text is inserted with the same value as the text. However, you can change it. SimpleComboBox_ItemInserting changes this logic so that, for any text starting with S, the value will be changed to an integer number. In Figure 20-8, you can see the results.

Typing the text into the first ComboBox and each by pressing Tab (use this): Five, Quarter, Six, Seven, Eight, Nine. Quarter starts with Q, so it is not inserted at all. All numbers are appended at the end of the list, except "Eight" because it starts with E. All numbers have the same value and text (check the text of the label of the combo) except "Nine," because it starts with N.

There are a few properties of ComboBox you can use to change the control's behavior. Table 20-2 summarizes them.

![](img/b5597c749e848b27b0d305153ae16106_961_0.png)

FIGURE 20-8: Checking the insertion logic of SimpleComboBox

# TABLE 20-2: ComboBox Properties

| PROPERTY | DESCRIPTION |
| --- | --- |
| DropDownStyle | Determines whether the user is to enter text that does not match an item in the list, and whether the list is always displayed. If DropList is specified, users are not allowed to enter text that does not match an item in the list. When DropDown (the default value) is specified, any text is allowed. If Simple is specified, any text is allowed and the list is always displayed, regardless of the AutoCompleteMode value. |
| CaseSensitive | Specifies whether user-typed text is matched to items in the list in a case-sensitive manner. The default is false. |
| RenderMode | Specifies whether the ComboBox is rendered as an Inline or Block level HTML element. The default is Inline. |
| ItemInsertLocation | Determines whether to Append or Prepend new items when they are inserted into the list, or whether to insert them in an Ordinal manner (alphabetically) based on the item Text or Value. The default is Append. |
| ListItemHoverCssClass | When specified, replaces the default style applied to highlighted items in the list with a custom CSS class. |
