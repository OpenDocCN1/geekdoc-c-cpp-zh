Step 1-8: Add the code from Figure 10-6 to the Click event handler of btnComputePrice. Run the form and test the code.

Use appropriate properties from Table 10-1 to add CheckBoxes to the items. Let the user select an item by checking the CheckBox for the item. Make necessary changes in the code to compute the total price. Test the code

It's time to practice! Do Exercise 10-1.

# ColumnClick Event: Selecting a Column

In addition to selecting a row, you also may select a column by clicking the column header, which triggers the ColumnClick event of the ListView. You may use this event to take an action when the user selects a column. Figure 10-7 shows the code within the ColumnClick event handler of the ListBox, to display the data item at the selected column of the selected row, in a Label named lblCurrentCell.

Figure 10-7: Code to get data from selected column

```
61
62    private void lvwShows_ColumnClick(object sender, ColumnClickEventArgs e)
63    {
64        int index = e.Column;
65        if (lvwShows.SelectedItems.Count > 0)
66            lblCurrentCell.Text = lvwShows.SelectedItems[0].SubItems[index].Text;
67    }
```

In line 64, the Column property of the parameter e gives the index of the selected column. The content of the cell in the selected column of the selected row is displayed in the Label, lblCurrentCell, as shown in Figure 10-8.

Figure 10-8: The ListViewApp form with content of current cell displayed

![](bbox=[0.09, 0.637, 0.732, 0.923])