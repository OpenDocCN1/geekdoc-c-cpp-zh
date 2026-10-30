```
' Retrieve an array of employee rows.
EmployeeDataRows = JobDataRow.GetChildRows(
    "EmployeeToJobsRelation")

' Fill the list with the array of employee rows.
EmployeeListBox.Items.Clear()
For Each EmployeeDataRow In EmployeeDataRows
    EmployeeListBox.Items.Add(
        EmployeeDataRow[FullName].ToString)
Next
Catch ex As Exception
    MessageBox.Show(ex.Message)
End Try
End Sub
End Class
```

# Feedback 4.3

+   1. Assume that a combo box displays store names and uses the stor_id property as a ValueMember. Write the statement(s) to filter the stores table using StoresBindingSource, selecting the record(s) that match a store selected from the list.

Use the following diagram for questions 2 and 3. Assume that a proper 1:M relationship, called ProductsToCategoriesRelation, has been set up between the categories and products tables. The DataSet is called ProductsDataSet and the data type of CategoryID and ProductID is Integer (Int32).

![](bbox=[0.25, 0.72, 0.62, 0.86])

+   2. The user selects a product name from a list box and you want to retrieve the category name. Write the statements to retrieve the category name and display it in a label.

+   3. Assuming the same proper relationship, write the statements to retrieve an array of all of the products in a selected category. Fill a list box with the array of products.

# Many-to-Many Relationships

Recall that a many-to-many relationship requires a third table, called a junction table. Figure 4.20 shows the relationships for the titles table and authors table, which are joined by the titleauthor table. Notice that au_id is the primary key in the authors table; a given au_id can appear only once. Similarly, title_id is the primary key of the titles table and any one title_id can appear only once. But in the junction table, titleauthor, any one au_id and any one title_id can appear any number of times. The combination of au_id and title_id