# The Category Maintenance application

![](bbox=[0.155, 0.097, 0.837, 0.456])

# Description

+   - The Category Maintenance application uses a ListView control to let the user update, delete, or insert rows in the Categories table.
+   - To edit a category, the user clicks the Edit button for that category. This places the row for that category into edit mode. The user can then change the Short Name or Long Name and click the Update button. Or, the user can click the Cancel button to leave edit mode without performing the update.
+   - To delete a category, the user clicks the Delete button for that category.
+   - To add a category, the user enters a Category ID, Short Name, and Long Name into the last row of the ListView control and then clicks the Insert button. Or, the user can click the Clear button to clear the entries without adding the category.
+   - If the user attempts to update or add a row with a column that is blank, an error message is displayed in a ValidationSummary control.