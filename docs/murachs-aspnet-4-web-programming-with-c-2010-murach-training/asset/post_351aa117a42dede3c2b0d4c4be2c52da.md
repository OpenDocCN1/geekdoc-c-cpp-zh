
## How to define the templates for a data list

Figure 13-12 shows you how to define the templates for a data list. The table in this figure lists the templates you’re most likely to use. Although you can also create templates that let the user select and edit items in the list, you’re not likely to use a DataList control for these functions. Instead, you’ll use the GridView, DetailsView, FormView, or ListView controls as described in the next three chapters.

The only template that’s required for a data list is the Item template, which defines how each item in the data source is displayed. Depending on the requirements of your application, though, you may need to use one or more of the other templates as well. For example, you’ll typically use a Header template to create headings that are displayed in the first row of the data list.

To define the templates for a data list, you work in *template-editing mode*. At the top of this figure, for example, you can see the Item template for a list that includes four columns. This template is displayed by default when you enter template-editing mode. To display a different template, you can use the Display drop-down list in the smart tag menu for the control. You can also display a group of related templates by selecting the group name from this list. For example, you can display both the Header and Footer templates by selecting the Header and Footer Templates item.

If a data list consists of two or more columns, you’ll want to place the text and controls in each template within a table. That way, you can set the width of each column in the data list by setting the widths of the columns in the table. In addition, if you add two or more templates to a data list, you can align the columns in the templates by setting the widths of the corresponding table columns to the same values. In this illustration, for example, I set the Width attributes of the corresponding columns in the Item template and the Header template to the same values.

Before I go on, you should realize that you use templates to define the content of a data list and not its appearance. For example, you use the AlternatingItem template to display different content for every other row in a data list, not to shade or highlight every other row. To format a data list, you use styles as shown in the next figure.

## 曹冲称象

三国时期，曹操得到一头大象。大象又高又大，身子像一堵墙，腿像四根柱子。

曹操问：“这头大象到底有多重呢？”官员们七嘴八舌地议论起来。

有人说：“得造一杆大秤，砍一棵大树做秤杆。”有人说：“有了大秤也不成，谁有那么大的力气提得起这杆大秤呢？”

> “大象太重了！怎么称呢？”

![](img/c024ccf88e28c30c07dd410d4342288f_447_0.png)

这时，曹操的儿子曹冲才七岁，他站出来说：“我有个办法。把大象赶到一艘大船上，在船身下沉的地方画一条线。再把大象赶上岸，往船上装石头，装到船沉到画线的地方为止。然后称一称船上的石头。石头有多重，大象就有多重。”

曹操微笑着点了点头。他叫人照曹冲说的办法去做，果然称出了大象的重量。

## The Format page of the Properties dialog box

![](img/c024ccf88e28c30c07dd410d4342288f_448_0.png)

### Common style elements for a data list

| Element | Description |
|---|---|
| HeaderStyle | The style used for the header. |
| FooterStyle | The style used for the footer. |
| ItemStyle | The style used for each item in the data source. |
| AlternatingItemStyle | The style used for alternating items in the data source. |
| SeparatorStyle | The style for the separator. |

### The asp tag for a Header style

```
<HeaderStyle BackColor="Black" Font-Bold="True" ForeColor="White" />
```

### Description

- You can format a data list by applying a predefined scheme, by using the Properties dialog box, by using the Properties window, or by editing the aspx code.
- To apply a scheme, choose Auto Format from the control’s smart tag menu and then select the scheme you want to apply.
- To use the Properties dialog box, choose Property Builder from the control’s smart tag menu and then set the properties for the data list and its templates.
- To use the Properties window to format a template, expand the style property for that template and then set its properties.

## How to use data binding

Once you’ve configured a data source control, you can bind it to a web form control to automatically display the data retrieved by the data source on the page. In the following topics, you’ll learn how to bind a list control to a data source and how to bind controls defined within the templates of another control like a DataList control.

### How to bind a list control to a data source

In chapter 6, you learned about the five list controls that you can use in an ASP.NET 4 application. Now, figure 13-14 shows you how you can bind any of these controls to a data source.

The table in this figure shows the three attributes you use to bind a list control to a data source. The DataSourceID attribute provides the ID of the data source. The DataTextField attribute provides the name of the data source field that’s displayed in the list. And the DataValueField attribute provides the name of the data source field that is returned by the SelectedValue property when the user selects an item from the list.

You can set these attributes manually by using the Properties window or by directly editing the aspx code. Or, you can use the Data Source Configuration Wizard shown at the top of this figure to set these properties. To do that, display the smart tag menu for the list and select Choose Data Source. Then, use the wizard’s controls to set the data source, display field, and value field.

The code example in this figure shows a drop-down list that’s bound to a data source named SqlDataSource1. The field named LongName provides the values that are displayed in the drop-down list, and the field named CategoryID supplies the value that’s returned by the SelectedValue property when the user selects an item from the list.

## The Data Source Configuration Wizard for binding a drop-down list

![](img/c024ccf88e28c30c07dd410d4342288f_450_0.png)

### List control attributes for data binding

| Attribute | Description |
|---|---|
| DataSourceID | The ID of the data source to bind the list to. |
| DataTextField | The name of the data source field that should be displayed in the list. |
| DataValueField | The name of the data source field whose value should be returned by the SelectedValue property of the list. |

### The aspx code for a drop-down list that’s bound to a SQL data source

```aspx
<asp:DropDownList ID="ddlCategory" runat="server"
    AutoPostBack="True"
    DataSourceID="SqlDataSource1"
    DataTextField="LongName"
    DataValueField="CategoryID">
</asp:DropDownList>
```

### Description

- You can bind any of the controls that inherit the ListControl class to a data source. That includes the list box control, the drop-down list control, the check box list control, the radio button list control, and the bulleted list control.
- You can use the Data Source Configuration Wizard to select the data source for a list control, the data field to display in the list, and the data value to return for the selected item.
- You can also use the DataTextFormatString attribute of a list control to specify a format string you want to apply to the text that’s displayed in the control.

Figure 13-14   How to bind a list control to a data source

## The DataBindings dialog box for binding a control

![](img/c024ccf88e28c30c07dd410d4342288f_452_0.png)

### The syntax of the Eval and Bind methods

```
<%# {Eval|Bind} (NameString [, FormatString]) %>
```

### Code examples

```
<%# Eval("Name") %>
<%# Eval("UnitPrice", "{0:C}") %>
<%# Bind("UnitPrice", "{0:C}") %>
```

### Description

- To bind a control in a template, select the Edit DataBindings command from the smart tag menu for the control to display the DataBindings dialog box. Then, select the property you want to bind to (usually Text), select the Field Binding option, and select the field you want to bind to from the Bound To drop-down list.
- If you want to apply a format to the bound data, select a format from the Format drop-down list.
- As you specify the binding for a control, Visual Studio generates a data binding expression that uses the Eval method. You can see this method in the Code Expression box at the bottom of the DataBindings dialog box.
- You can also create a custom binding expression by selecting the Custom Binding option and then entering the expression in the Code Expression text box.
- The Eval method provides only for displaying data from a data source in a control. In contrast, the Bind method provides for two-way binding, which means that it can be used to display as well as update data from a data source.

### Note

- If the Field Binding option isn’t enabled, you can click the Refresh Schema link and then click the OK button in the dialog box that’s displayed to enable it.

Figure 13-15   How to bind the controls in a template
