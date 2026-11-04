# Part II: Application Development Using C#

The source of the LinqDataSource control now looks like this:

```
<asp:LinqDataSource
    ID="LinqDataSource1"
    runat="server"
    ContextTypeName="DataClassesDataContext"
    EnableDelete="True"
    EnableInserts="True"
    EnableUpdate="True"
    TableName="titles"
    Where="pub_id = @pub_id">
    <WhereParameters>
        <asp:ControlParameter
            ControlID="DropDownList1"
            Name="pub_id"
            PropertyName="SelectedValue"
            Type="String" />
    </WhereParameters>
</asp:LinqDataSource>
```

Press F5 to debug the application. When you select a publisher now, all books published by that publisher are displayed in the GridView control (see Figure 17-20).

![](bbox=[0.15, 0.62, 0.85, 0.82])

Figure 17-20