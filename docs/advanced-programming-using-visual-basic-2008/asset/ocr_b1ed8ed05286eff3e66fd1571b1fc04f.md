individual database fields, because many professional applications use that approach.

When you allow the user to select a value from a bound combo box, you write the code to retrieve the data in the SelectionChangeCommitted event handler. There are basically three steps in the process:

+   1. Find the row in the employee table that matches the combo box selection.

+   2. Use the GetParentRow method to retrieve the matching row from the jobs table.

+   3. Retrieve the specific data item and assign it to the Text property of a text box.

> TIP
> Add Imports System.Data before the Class statement; then you can omit the "Data." namespace on all declarations for data objects in code.

# Find the Employee (Child) Row

Declare a DataRow object for the employee table and another one for the jobs table.

```
Dim EmployeeDataRow As DataRow
Dim JobDataRow As DataRow
```

Use the SelectedValue from the employee combo box to find the complete employee record. Each table in the DataSet contains a method to find records by the key field. Since the primary key in the employee table is emp_id, the FindByemp_id method is automatically generated for the table object.
The format for the find is

```
DataRow = DataSetName.TableName.FindByMethod(PrimaryKeyValue)
```

If you set up the combo box ValueMember property as emp_id, then you can use this code to retrieve the correct employee record by its key field.

```
' Save the Employee ID for the selected employee.
EmployeeIDString = EmployeeComboBox.SelectedValue.ToString
' Find the data row for this employee.
EmployeeDataRow = PubsDataSet.employee.FindByemp_id(EmployeeIDString)
```

# Get the Parent Row

Now that you know the row in the employee (child) table that matches the combo box entry, you must get the parent row from the jobs table.

```
' Find the matching row from the parent (jobs) table.
JobDataRow = EmployeeDataRow.GetParentRow("EmployeeToJobsRelation")
```

Note that "EmployeeToJobsRelation" in the GetParentRow method argument is the name of the relation that we discussed setting up in Figure 4.16.

# Retrieve a Specific Field

The final step is to get the field from the data row.

```
' Display a field from the matching row.
JobTitleTextBox.Text = JobDataRow!job_desc.ToString
```