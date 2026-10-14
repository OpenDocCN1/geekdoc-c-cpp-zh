# A GridView control that provides for paging

| ID | Name | Category | Unit Price | On Hand |
|---|---|---|---:|---:|
| pow01 | Austin Powers | costumes | $79.99 | 25 |
| blo01 | Black Light (24") | fx | $24.99 | 200 |
| vader01 | Darth Vader Mask | masks | $19.99 | 100 |
| cat01 | Deranged Cat | props | $19.99 | 45 |
| bats01 | Flying Bats | props | $69.99 | 25 |
| fogj01 | Fog Juice (1qt) | fx | $9.99 | 500 |
| fog01 | Fog Machine | fx | $34.99 | 100 |
| frank01 | Frankenstein | costumes | $39.99 | 100 |
|  | >>> |  |  |  |

# Attributes of the ObjectDataSource control that are used for paging

| Attribute | Description |
|---|---|
| EnablePaging | True if the ObjectDataSource control supports paging. |
| StartRowIndexParameterName | The name of the parameter in the select method of the data access class that receives the index of the first row to be retrieved. The default is startRowIndex. |
| MaximumRowsParameterName | The name of the parameter in the select method of the data access class that receives the maximum number of rows to be retrieved. The default is maximumRows. |
| SelectCountMethod | The name of a public method in the data access class that returns the total number of rows that are retrieved by the select method. |

# The aspx code for an ObjectDataSource control that provides for paging

```
```aspx
<asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
    SelectMethod="GetProductsByPage" TypeName="ProductDB"
    EnablePaging="True" StartRowIndexParameterName="startIndex"
    SelectCountMethod="SelectCount" MaximumRowsParameterName="maxRows">
</asp:ObjectDataSource>
```
```

# Description

+   - To use paging with a control like a GridView control that’s bound to an object data source, you must set the four attributes of the ObjectDataSource control shown above.
+   - When a pager control on a bound control is clicked, the index of the starting row to be displayed and the maximum number of rows to be displayed are passed to the ObjectDataSource control. The ObjectDataSource control then passes these values to the parameters of the select method specified by the StartRowIndexParameterName and MaximumRowsParameterName attributes of the control.
+   - In addition to the select method that’s used to retrieve the rows to be displayed, the data access class must include a method that returns the total number of rows that are retrieved. This method is named on the SelectCountMethod attribute of the ObjectDataSource control, and it’s used by the bound control to determine what pager controls to display.

Figure 17-16    How to create an object data source that provides for paging