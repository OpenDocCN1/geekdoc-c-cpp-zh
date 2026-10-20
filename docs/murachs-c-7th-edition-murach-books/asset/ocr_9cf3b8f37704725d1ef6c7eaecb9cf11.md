# A DataGridView control after it’s added to a form

![](bbox=[0.155, 0.115, 0.815, 0.45])

# Properties that you can set from the smart tag menu

| Property | Description |
|---|---|
| AllowUserToAddRows | If set to true, users can add rows directly to the grid. Otherwise, they can’t. The default is true. |
| AllowUserToDeleteRows | If set to true, users can delete rows directly from the grid. Otherwise, they can’t. The default is true. |
| AllowUsersToOrderColumns | If set to true, users can manually reposition columns. Otherwise, they can’t. The default is false. |
| ReadOnly | If set to true, users can’t edit data directly in the grid. Otherwise, they can. The default is false. |

# Description

+   - When you first add a DataGridView control to a form, its smart tag menu is displayed. You can use the options in this menu to determine if users can add, edit, and delete data directly in the control and if they can reorder columns.
+   - You can also determine the functions provided by the DataGridView control by using code to set the properties shown above.
+   - When you set the data source for a DataGridView control in code as shown in this chapter, you can’t choose the data source from the smart tag menu. In addition, you can’t edit or add columns using the commands available from this menu.

Figure 22-2    How to set the functions provided by a DataGridView control