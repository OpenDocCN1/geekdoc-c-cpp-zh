# SelectWizard Project

# SQL Server Database Programming with C#

| CSE_DEPTDataSet.FacultyRow | UpFactoryRow(ref FacultyRow fRow) |

```
private CSE_DEPTDataSet.FacultyRow UpFactoryRow(ref CSE_DEPTDataSet.FacultyRow fRow)
{
    byte[] image;
    image = getImage();
    fRow.name = txtFacultyName.Text;
    fRow.office = txtOffice.Text;
    fRow.phone = txtPhone.Text;
    fRow.title = txtTitle.Text;
    fRow.college = txtCollege.Text;
    fRow.email = txtEmail.Text;
    fRow.image = image;
    return fRow;
}
```

**FIGURE 7.8** codes for the user-defined method UpFactoryRow().

+   C. A user-defined method **UpFactoryRow** will be built later to assign all updated faculty information to the selected row. In this way, the faculty information, exactly a row in the **Faculty** table in DataSet, is updated.
D. The **Validate()* command allows the editing of a control. In our case, it allows any editing for TextBox in the Form window.
E. The **EndEdit()* method of the binding source writes any edited data back to the controls in the data. In our case, any updated data entered into the TextBox will be reflected in the associated column in the DataSet.
F. Finally, the **Update()* method of the Table sends updated data back to the database. The argument of this method can be either a DataSet, a DataTable in the DataSet or a DataRow in a DataTable. In our case, we used the Faculty DataTable as the argument for this method.

The codes for the user-defined method **UpFactoryRow()* are shown in Figure 7.8. The functionality of this method is straightforward and easy to understand.
The argument of this method is a DataRow object and it is passed by a Reference to the method.
The advantage of using this method is that any modifications performed to DataRow object inside the method can be returned to the calling procedure without requiring the creation of another returned value. The updated faculty information stored in the associated TextBox is assigned to the DataRow in the *Faculty* table in the DataSet. In this way, the selected DataSet in the **Faculty** table is updated.
At this point, we finished the coding development for two methods to update the data in a database. Next is how to delete data from the database.

# 7.2.4 Develop Code to Delete Data Using the TableAdapter DBDirect

To delete data from a database, you can use either the TableAdapter DBDirect method **tableAdapter.Update()]* method. Or, if your application uses TableAdapters, you can use the run time method to create a command to delete data from a database (for example, **ExecuteQuery()*).

The **TableAdapter.Delete()* is typically used when your application uses a DataSet to store data, whereas the TableAdapter.Delete is typically used when your application uses objects, for example in our case we used TextBoxes, to store data.
As mentioned in the previous section, to delete a record from our sample database, no user interface is needed and we can use the Form window to perform this data deleting