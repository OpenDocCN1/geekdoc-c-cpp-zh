
# Games

| Name | ReleaseDate | Played | PlayerScores | GameCategory |
|---|---|---|---|---|
| INVADERS | 1/1/1982 12:00:00 AM | | ViewPlayerScores | Space |
| WONDERBOY | 12/23/1982 05:00:00 AM | | ViewPlayerScores | Arcade |

the ForeignKey.ascx template, in the DynamicData/Filters folder. it uses the DDFilter CSS class.

You can also check the CSSClass used by a specific control in a template. For example, the following code corresponds to

```csharp
<% Control Language="C*" CodeFile="ForeignKey.ascx"
Inherits="ForeignKey" %>

<asp:DropDownList runat="server" Id="DropDownList1" AutoPostBack="True"
CssClass="DDFilter"
OnChanged="DropDownList1_SelectedIndexChanged">
<asp:ListItem Text="All" Value="*" />
</asp:DropDownList>
```

The default definition for this class is as follows:

```css
.DDFilter{
font: .95em Tahoma, Arial, Sans-serif;
color:#666;
}
```

The new version for the code that defines the aforementioned class in the Site.css file applies an aqua background color and uses a bold font to emphasize the combo box:

```css
.DDFilter{
font: .95em Tahoma, Arial, Sans-serif;
font-weight: bold;
background-color: Aqua;
}
```

> You can check the CSSClass used by the different controls in the templates and make the necessary changes to adapt the look and feel of the website to your needs.

The default title and header for all the pages that compose a Dynamic Data is Dynamic Site, and this is defined in the Site.master file. You can change this file to customize the title and the header.

For example, Listing 17-2 shows a customized version of the file with Retro-gamers championship as the new title and header. The code that was changed appears in bold.

# LISTING 17-2: A New Title and Header in the Site.master File

```aspx
<%@ Language="C#" CodeFile="Site.master.cs" Inherits="Server" %>
<!DOCTYPE html HTML "//W3C//DTD HTML 1.0 Transitional//EN"
EN "http://www.w3.org/TR/xhtml/html-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<Head runat="server">
<title>Retro-gamers Championship</title>
<link href="Site.css" rel="stylesheet" type="text/css" runat="server" />
<asp:ContentPlaceHolder id="header" runat="server" />
<asp:ContentPlaceHolder>
</Head>
<body>
<h1 class="DDHeader">Retro-gamers championship</h1>
<div class="Navigation">
<a runat="server" href="/"><img alt="Back to home page" runat="server" src="DynamicData/Content/Images/back.gif" />Back to home page</a>
</div>
<form id="form1" runat="server">
<div>
<!-- TODO: Enable partial rendering by setting the attribute to "true" to provide a smoother browsing experience.
Leaving partial rendering disabled will provide a better paging experience while the application is in development. -->
<asp:ScriptManager Id="ScriptManager1" runat="server"
EnablePartialRendering="false"/>

<asp:ContentPlaceHolder id="ContentPlaceHolder1" runat="server" />
</asp:ContentPlaceHolder>
</div>
</form>
</body>
</html>
```

Also, the default title displaying the available tables and views My Tables, and this is defined in the Default.aspx file. You can change this file to customize the header.

For example, Listing 17-3 shows a customized version of the file with Click on the desired entity name as the header. The code that changed appears here in bold.

# LISTING 17-3: A New Header in the Default.aspx File

```aspx
<% Page Language="C#" MasterFile="~/Site.master" 
CodeFile="Default.aspx" Inherits="_Default" %>
<asp:Content Id="head" ContentHolderID="head" Runat="Server">
</asp:Content>
<asp:Content Id="Content1" ContentHolderID="ContentHolder1">
<asp:ScriptManager Id="ManagerProxy1" runat="server" />
<h2 id="DDSubHeader">Click on the desired entity name</h2>
<br /> /><br />
<asp:GridView Id="Menu1" runat="server" AutoGenerateColumns="false" 
Style-CssClass="DDGridView" RowStyle-CssClass="td"
HeaderStyle-CssClass="td" CellPadding="6">
<Columns>
  <asp:TemplateField HeaderText="Table Name" SortExpression="TableName">
  <ItemTemplate>
    <asp:DynamicHyperLink Id="HyperLink1" runat="server">
    #Eval("DisplayName") %>
    </asp:DynamicHyperLink>
  </ItemTemplate>
  </asp:TemplateField>
</Columns>
</asp:GridView>
</asp:Content>
```

Code file [RetroGamesWeb2/Default.aspx] available for download at Wrox.com.

Also, you will want to customize the CSS styles used for each element. Figure 17-26 shows the results of the changes.

# Working with Page Templates

In the example shown, the web browser is using the ListDetails.aspx template to display the combined-mode with in-line editing. You can make the necessary changes to this page, found in the DynamicData/PageTemplates folder.

![](img/b5597c749e848b27b0d305153ae16106_777_0.png)

**FIGURE 17-26:** Page with new title and header

For example, you can use alternating background colors by following these steps:

1. Open the Site.css file.
2. Add a new style to define a background color for alternating rows:
```css
table.DDGridView {
    background-color: Aqua;
}
```
3. Now, open the ListDetails.aspx page template and switch to Design view.
4. Click on the GridView. Go to its properties and enter the AlternatingStyle. The GridView will apply the previously defined style to alternating rows. The design view will display an aqua background in the different rows, as shown in Figure 17-27.

![](img/b5597c749e848b27b0d305153ae16106_778_0.png)

Figure 17-27: Applying a previously defined style to alternating rows

Figure 17-28 shows the results of applying the new CSS style to the grid when the website displays data from the PlayerScores table.

![](img/b5597c749e848b27b0d305153ae16106_778_1.png)

Figure 17-28: Applying the new CSS style in the grid

> It is possible to edit the other page templates to customize the presentation of different controls and their behavior as explained in the previous example. However, it is very important to keep the necessary basic structure to make these templates work with Dynamic Data.

Table 17-5 describes the five page templates provided by Dynamic Data.

### TABLE 17-5: Page Templates

| FILE | DESCRIPTION |
| --- | --- |
| Details.aspx | Shows the detailed view of a single record. It uses a DetailsView control. |
| Edit.aspx | Allows the user to edit a single record. It uses a Details control. |
| Insert.aspx | Lets the user insert a new record. It uses a DetailsView control. |
| List.aspx | Displays lists of records using a grid and provides combo boxes to filter data. It uses GridView, GridPager, and DropList controls. |
| ListDetails.aspx | Displays lists of records using a grid, provides combo boxes to filter data and enables in-line editing and visualization of details in the same page. It uses GridView, GridPager, and DropList controls. |

# Working with Field Templates

ASP.NET Dynamic Data uses field templates to render the data in data-bound controls. They are user controls derived from the FieldTemplateControl class (System.Web.DynamicData.FieldTemplateControl) that maps fields in the data-bound to data types in the data model. The Dynamic Data framework identifies the data type for the field at run-time, and then checks for the appropriate field template to render the data in the data-bound control.

The field template to be used in each case depends on the data type and the mode — display, edit, or insert. Some field templates provide a specific edit or insert template than the one used for the display mode. For example, the DateTime.ascx template is used for displaying a DateTime data type. However, when editing or inserting, the DateTime_Edit.ascx is used.

You can make the necessary changes to an existing field template, found in the DynamicData/FieldTemplates. For example, you can change the default CSS class for the DataType field template when it is running in the edit mode by these steps:

1. Open the Site.css file.
2. Add a new style to add a background color for the control, TextBox:
```css
.DTextBoxEdit
{
  background-color: #000FF;
  color: #FFFFFF;
  font-weight: bold;
}
```
3. Now, add the DateTime_Edit.ascx field template and replace CssClass="DTextBox" with CssClass="DTextBoxEdit", as shown in Listing 17-4. This, the textbox displayed when editing the DataType data type will apply the previously defined style to use a different background. You can check it by editing a row from the Game table, as shown in Figure 17-27.

| Score | 7500 |
| ScoreDate | 1/7/2009 12:00:00 AM |
| Game | WONDERBOY |
| Player | KEVIN KONG |
| Update | Cancel |

LISTING 17-4: A Customized DateTime_Edit.ascx.

```csharp
<% Control Language="C#" CodeFile="DateTime_Edit.ascx"
Inherits="DynamicEditField" %>
```

```aspx
<asp:TextBox ID="TextBox1" runat="server" CssClass="DTextBoxEdit">
  <asp:FieldEdit ValueString="#" Columns="20" />
</asp:TextBox>
```

```aspx
<asp:RequiredValidator runat="server" ID="RequiredFieldValidator1"
CssClass="DDControlValidator" ControlToValidate="TextBox1"
Display="Dynamic" Enabled="false" />
```

```aspx
<asp:RegularValidator runat="server" ID="RegularValidator1"
CssClass="DDControlValidator" ControlToValidate="TextBox1"
Display="Dynamic" Enabled="false" />
```

```aspx
<asp:DynamicValidator runat="server" ID="DynamicValidator1"
CssClass="DDControlValidator" ControlToValidate="TextBox1"
Display="Dynamic" 
CustomValidator runat="server" ID="DateValidator"
CssClass="DDControlValidator" ControlToValidate="TextBox1"
EnableClientScript="false" Enabled="false"
OnServerValidate="Validator_ServerValidate" />
```

```text
Code file [/RetroGamesWeb2/FieldTemplates/DateTime_Edit.ascx] as available at Wrox.com
```

FIGURE 17-29: Editing a row

![](img/b5597c749e848b27b0d305153ae16106_780_0.png)
