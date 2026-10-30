If you add records to external linked tables, create a form to add records and set the DataEntry property to True. This makes the form an entry form that starts with a blank record every time it's executed. Data entry forms are not pre-populated with data from the bound table. Using a dedicated data entry form is much more efficient than building a normal form, populating it with data from the linked source, and then moving to the end of the linked data just to add a new record.

# Deleting a linked table reference

Deleting a linked table from your database is a simple matter of performing three steps:

+   1. In the Navigation pane, select the linked table you want to delete.
+   2. Press the Delete key, or right-click the linked table and select Delete from the shortcut menu.
+   3. Click OK in the Access dialog box to delete the file.

> NOTE
> Deleting an external table deletes only its name from the database object list. The actual data is not deleted from its source location.

# Viewing or changing information for linked tables

Use the Linked Table Manager to update the links when you move, rename, or modify tables, indexes, or relationships associated with linked tables. Otherwise, Access won't be able to find the data file referenced by the link.

+   1. Select the External Data tab of the Ribbon and click the Linked Table Manager button. The Linked Table Manager (shown in Figure 7.14) appears, letting you locate the data files associated with the linked tables in the database.
+   2. Click the check box next to a linked table and click OK.
+   3. Find the missing file and relink to Access. If all the files are already linked correctly, clicking OK makes Access verify all the linkages associated with all the selected tables.
+   4. If you know all the linked data sources have been moved, select the Always Prompt for New Location check box, and then click OK. Access then prompts you for the new location and links all the tables as a batch process. This is much faster than linking one or two tables at a time. If all your tables come from different sources, though, the Linked Table Manager still requires you to select each source one at a time.