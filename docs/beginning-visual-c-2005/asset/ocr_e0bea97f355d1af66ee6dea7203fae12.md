![](bbox=[0.33, 0.08, 0.61, 0.42])

# Figure 22-21

The top three menu items enable you to choose the controls to be used with the table when you add the data source to the form. If you click the DataGridView item from the menu, you are selecting that control as the one to be for displaying the table, whereas clicking on the Details item indicates you want one control per table column. If you click the [None] item, you are indicating you want no controls to be created when you add the data source to the form. The last menu item opens a dialog box for changing the default control for the table from the current default of DataGridView and for customizing the choice of controls. In this instance, you should just click Details because you want one control for each table column.

You now have to decide which control you want to use for each table column. You can extend the tree that shows the column names in the Order Details table name by clicking the + symbol to the left of the table name. If you then click the first column name to select it, you'll see that you can display a menu for that, too, by clicking the down arrow. The menu is shown in Figure 22-22.

You can choose any of the controls shown in the menu, but I suggest a TextBox control is most appropriate for the OrderID column. You need to repeat the process for each table column; you can choose a NumericUpDown control for the Quantity column and select a TextBox control for each of the others.

Note that selecting the Customize menu option in the Data Sources pane shown in Figure 22-22 displays the Options dialog box in which you can change the selection of controls available for displaying different types of data. You can also change the control to be selected by default when you drag an item from the Data Sources pane to a form. Figure 22-23 shows the Options dialog box.