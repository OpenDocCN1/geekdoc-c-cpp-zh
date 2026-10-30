can always add new fields to a table without problems, but changing existing fields might be an issue. And, with very few exceptions, it's almost always a bad idea to change a field's name after a table has been put into use in an application.

# Inserting a new field

To insert a new field, in the Table Design window, place your cursor on an existing field, right-click on a field in the table's design surface, and select Insert Rows, or just click the Insert Rows button on the Design tab of the Ribbon. A new row is added to the table, and existing fields are pushed down. You can then enter a new field definition. Inserting a field doesn't disturb other fields or existing data. If you have queries, forms, or reports that use the table, you might need to add the field to those objects as well.

# Deleting a field

There are three ways to delete a field. While the table is in Design view:

+   - Select the field by clicking the row selector and then press Delete.
+   - Right-click the selected field and choose Delete Rows from the shortcut menu.
+   - Select the field and click the Delete Rows button from the Tools group on the Design tab of the Ribbon.

When you delete a field containing data, you'll see a warning that you'll lose data in the table for the selected field. If the table contains data, make sure that you want to eliminate the data for that field (column). You'll also have to delete the same field from queries, forms, reports, macros, and VBA code that use the field name.

> TIP
> If you try to delete a field that's part of a relationship (a primary or secondary key field), Access informs you that you can't delete the field until you remove the relationship in the Relationships window.
> Table relationships and the Relationships window are discussed in Chapter 4.

If you delete a field, you must also fix all references to that field throughout Access. Because you can use a field name in forms, queries, reports, and even table data validation, you must examine your system carefully to find any instances in which you might have used the specific field name.

# Changing a field location

The order of your fields, as entered in the table's Design view, determines the left-to-right column sequence in the table's Datasheet view. If you decide that your fields should be rearranged, click on a field selector and use the mouse to drag the field to its new location.

# Changing a field name

You change a field's name by selecting the field's name in the Table Design window and entering a new name. Access updates the table design automatically. As long as you're