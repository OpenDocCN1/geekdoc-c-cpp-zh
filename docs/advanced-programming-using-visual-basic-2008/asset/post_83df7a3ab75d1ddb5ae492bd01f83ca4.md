
**Figure 4.15**

The jobs and employee tables in the DataSet Designer. The jobs table is the one side of the one-to-many relationship.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_190_0.png)

Right-click the relation line, and select Edit Relation. In the Relation dialog box (Figure 4.16), you can view and modify the relationship. The default name for a relation is rather cryptic: "FK__employee__job_id__1BFD2C07" in this example. Change the name to something more meaningful, such as "EmployeeToJobsRelation," before you write any code that refers to the relation.

**Figure 4.16**

Change the name of the relation to something more meaningful than the default name, such as EmployeeToJobsRelation.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_190_1.png)

## Referring to Records and Fields

When you are working with data from a DataSet, you often want to refer to an individual field from a selected record. The actual data values are held in DataRow objects. Each Table object in a DataSet has a DataRows collection made up of DataRow objects (Figure 4.17).

**Figure 4.17**

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_191_0.png)

A Table object has a DataRows collection that consists of one DataRow object for each record in the table.

The data values are held in the DataRow.Item property. You can refer to the individual fields by index position (the first field is index 0), by field name enclosed in quotes, or with an exclamation mark (called the "bang"). For example, you can use any of these three statements to retrieve the fname field of this employee DataRow object:

```
FirstNameString = EmployeeDataRow.Item(1).ToString
FirstNameString = EmployeeDataRow.Item("fname").ToString
FirstNameString = EmployeeDataRow!fname.ToString
```

Unless you want to look up the index position of each field in a record, you'll find that using field names is much preferred. You can find the field names in the DataSet Designer and the Data Sources window.

## Retrieving a Related Parent Row

The following example allows the user to select an employee name from a bound combo box and then displays the hire date from the employee table and the job description from the jobs table (Figure 4.18). The data fields are displayed in unbound text boxes; that is, no data bindings exist for the text boxes. Each field is assigned to the Text property of a text box.

> Note: This application could easily be written using bound controls. The point of the exercise is to learn to use unbound controls and to refer to individual database fields, because many professional applications use that approach.

**Figure 4.18**

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_191_1.png)

From the selected employee name, the program retrieves the correct employee DataRow and the matching jobs parent DataRow to display the job description.

When you allow the user to select a value from a bound combo box, you write the code to retrieve the data in the SelectionChangeCommitted event handler. There are basically three steps in the process:

1. Find the row in the employee table that matches the combo box selection.
2. Use the GetParentRow method to retrieve the matching row from the jobs table.
3. Retrieve the specific data item and assign it to the Text property of a text box.

> **TIP**
> Add Imports System.Data before the Class statement; then you can omit the "Data." namespace on all declarations for data objects in code.

### Find the Employee (Child) Row

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

### Get the Parent Row

Now that you know the row in the employee (child) table that matches the combo box entry, you must get the parent row from the jobs table.

```
' Find the matching row from the parent (jobs) table.
JobDataRow = EmployeeDataRow.GetParentRow("EmployeeToJobsRelation")
```

Note that "EmployeeToJobsRelation" in the GetParentRow method argument is the name of the relation that we discussed setting up in Figure 4.16.

### Retrieve a Specific Field

The final step is to get the field from the data row.

```
' Display a field from the matching row.
JobTitleTextBox.Text = JobDataRow!job_desc.ToString
```

### The Complete Find Parent Program

```
'Program: Ch04FindParentUnbound
'Programmer: Bradley/Millspaugh
'Date: June 2009
'Description: Allow the user to select the employee name from a combo box
' and display the corresponding hire date from the same table
' and the job description from the jobs table.
' Demonstrates finding a parent row for a selected child row,
' referring to individual fields in a DataRow object, and
' assigning database fields to unbound controls.

Imports System.Data

Public Class EmployeeForm

Private Sub EmployeeForm_Load(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles MyBase.Load
' Fill the DataSet.
JobsTableAdapter.Fill(PubsDataSet.jobs)
EmployeeTableAdapter.Fill(PubsDataSet.employee)
End Sub

Private Sub EmployeeComboBox_SelectionChangeCommitted(ByVal sender As Object, _
ByVal e As System.EventArgs) _
Handles EmployeeComboBox.SelectionChangeCommitted
' Find and display the selected record.
Dim EmployeeIDString As String
Dim EmployeeDataRow As DataRow
Dim JobDataRow As DataRow

' Find the data row for the selected name.
EmployeeIDString = EmployeeComboBox.SelectedValue.ToString
EmployeeDataRow = PubsDataSet.employee.FindByemp_id( _
EmployeeIDString)

' Display a field from the selected row.
HireDateTextBox.Text = EmployeeDataRow.hire_date.ToString
' Use this alternate statement to format the date.
HireDateTextBox.Text = Convert.ToDateTime( _
EmployeeDataRow.hire_date).ToString("d")

' Find the matching row from the parent (jobs) table.
JobDataRow = EmployeeDataRow.GetParentRow( _
"EmployeeToJobsRelation")

' Display a field from the matching row.
JobTitleTextBox.Text = JobDataRow.job_desc.ToString
End Sub
End Class
```

## Retrieving Related Child Rows

Retrieving related child rows is similar to retrieving a related parent row. The primary difference is that the GetChildRows method returns an array of rows rather than a single row. In this variation on the previous program, the user selects a job title from the combo box. The program retrieves the correct data row for the job and displays the array of matching employees in a list box (Figure 4.19). Note that the DataSet and relationship in this program are exactly the same as in the preceding example.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_194_0.png)

**Figure 4.19**

When the user selects the job title (the parent), the program retrieves and displays an array of the matching employee (child) records.

### The Complete Find Children Program

```
'Program: Ch04FindChildrenUnbound
'Programmer: Bradley/Millspaugh
'Date: June 2009
'Description: Allow the user to select the job description from a
'combo box and display the corresponding employees
'(child rows) from the employee table.
'Demonstrates finding child rows for a selected parent row,
'referring to individual fields in a DataRow object, and
'assigning database fields to unbound controls.
'
Imports System.Data

Public Class EmployeeForm

Private Sub EmployeeForm_Load(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles MyBase.Load
'This line of code loads data into the 'PubsDataSet.jobs' table.
Me.JobsTableAdapter.Fill(Me.PubsDataSet.jobs)
'This line of code loads data into the 'PubsDataSet.employee' table.
Me.EmployeeTableAdapter.Fill(Me.PubsDataSet.employee)
End Sub

Private Sub JobComboBox_SelectionChangeCommitted(ByVal sender As Object, _
ByVal e As System.EventArgs) Handles JobComboBox.SelectionChangeCommitted
'Find and display employees for the selected job.

Dim JobIDShort As Short
Dim JobDataRow As DataRow
Dim EmployeeDataRow As DataRow
Dim EmployeeDataRows As DataRow()

Try
'Get the job_id of the selected job.
JobIDShort = Convert.ToInt16(JobComboBox.SelectedValue)
'Find the row from the job table for the selected job_id.
JobDataRow = PubsDataSet.jobs.FindByjob_id(JobIDShort)
```
