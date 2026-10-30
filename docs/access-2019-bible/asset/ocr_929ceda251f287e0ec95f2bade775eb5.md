# Using AutoNumber fields

Access gives special considerations to AutoNumber fields. You can’t change a previously defined field from another type to AutoNumber if any data has been added to the table. If you try to change an existing field to an AutoNumber, you’ll see an error that says:

> Once you enter data in a table, you can't change the data type of any field to AutoNumber, even if you haven't yet added data to that field.

You’ll have to add a new AutoNumber field and begin working with it instead of changing an existing field to AutoNumber.

> **NOTE**
> Only one AutoNumber field can be added to an Access table. Generally speaking, it’s better to use AutoNumber fields where their special characteristics are needed by an application.

# Completing tblCustomers

With tblCustomers in Design view, you’re ready to finalize its design. Table 3.1, shown earlier in this chapter, lists the field definitions for tblCustomers. Enter the field names and data types as shown in Table 3.1. The next few pages explain how to change existing fields (which includes rearranging the field order, changing a field name, and deleting a field).

Here are the steps for adding fields to a table structure:

+   1. Place the cursor in the Field Name column in the row where you want the field to appear.
+   2. Enter the field name and press Enter or Tab to move to the Data Type column.
+   3. Select the field’s data type from the drop-down list in the Data Type column.
+   4. If desired, add a description for the field in the Description column.

Repeat each of these steps to create each of the data entry fields for tblCustomers. You can press the down arrow (↓) key to move between rows, or use the mouse and click on any row. Pressing F6 switches the focus from the top to the bottom of the Table Design window, and vice versa.

# Changing a Table Design

Even the best planned table may require changes from time to time. You might find that you want to add another field, remove a field, change a field name or data type, or simply rearrange the order of the field names.

Although a table’s design can be changed at any time, special considerations must be given to tables containing data. Be careful of making changes that damage data in the table, such as making text fields smaller or changing the Field Size property of Number fields. You