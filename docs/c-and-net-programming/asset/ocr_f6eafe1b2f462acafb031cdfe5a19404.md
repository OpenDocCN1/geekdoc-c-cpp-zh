# 7) Customizing a DataList control at run time

1) At run time using the ListItemType property in the ItemCreated event the DataList control can be customized, as shown below,

```
private void DataList1_ItemCreated(object sender, ..........System.Web.UI.WebControls.
{
    switch (e.Item.ItemType)
    {
        case System.Web.UI.WebControls.ListItemType.Item :
            e.Item.BackColor = Color.Blue;
            break;
        case System.Web.UI.WebControls.ListItemType.AlternatingItem :
            e.Item.BackColor = Color.Red;
            break;
        case System.Web.UI.WebControls.ListItemType.SelectedItem :
            e.Item.BackColor = Color.Green;
            break;
        default :
            break;
    }
}
```

# 8) The Styles that can be used with DataList control are,

+   1) AlternatingItemStyle
+   2) EditItemStyle
+   3) FooterStyle
+   4) HeaderStyle
+   5) ItemStyle
+   6) SelectedItemStyle
+   7) SeparatorStyle

These styles can be used to format the control, that is, format the HTML code that is rendered.

# 9) Layouts of the DataList control can be used for formatting, that is, further customization of user interface can be done. The available layouts are,

+   1) FlowLayout
+   2) TableLayout
+   3) VerticalLayout
+   4) HorizontalLayout

4) Flow or table format can be specified at design time by specifying the following in the .aspx file.