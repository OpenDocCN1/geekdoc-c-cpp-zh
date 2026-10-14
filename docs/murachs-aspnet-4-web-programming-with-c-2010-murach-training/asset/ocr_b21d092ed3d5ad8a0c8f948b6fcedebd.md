# Column field elements

| Element | Description |
|---|---|
| Columns | The columns that are displayed by a GridView control. |
| asp:BoundField | A field bound to a data source column. |
| asp:ButtonField | A field that displays a button. |
| asp:CheckBoxField | A field that displays a check box. |
| asp:CommandField | A field that contains Select, Edit, Delete, Update, or Cancel buttons. |
| asp:HyperlinkField | A field that displays a hyperlink. |
| asp:ImageField | A field that displays an image. |
| asp:TemplateField | Lets you create a column with custom content. |

# Style elements

| Element | Description |
|---|---|
| RowStyle | The style used for data rows. |
| AlternatingRowStyle | The style used for alternating data rows. |
| SelectedRowStyle | The style used when the row is selected. |
| EditRowStyle | The style used when the row is being edited. |
| EmptyDataRowStyle | The style used when the data source is empty. |
| ItemStyle | The style used for an individual field. |
| HeaderStyle | The style used to format the header row. |
| FooterStyle | The style used to format the footer row. |
| PagerStyle | The style used to format the pager row. |

# The aspx code for a control that uses field and style elements

```
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" DataKeyNames="CategoryID" DataSourceID="SqlDataSource1">
  <Columns>
    <asp:BoundField DataField="CategoryID" HeaderText="ID" ReadOnly="true" >
      <ItemStyle Width="100px" />
    </asp:BoundField>
    .
    .
  </Columns>
  <HeaderStyle BackColor="LightGray" ForeColor="White" Font-Bold="True" />
  <RowStyle BackColor="White" ForeColor="Black" />
  <SelectedRowStyle BackColor="Gray" ForeColor="White" Font-Bold="True" />
  <FooterStyle BackColor="LightGray" ForeColor="Blue" />
  <PagerStyle BackColor="LightGray" ForeColor="Blue" HorizontalAlign="Center" />
</asp:GridView>
```

# Description

+   - The GridView control uses several child elements to define the column fields in a row and the styles used to format the data.