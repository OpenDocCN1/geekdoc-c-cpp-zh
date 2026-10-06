```
employeeModel->select();
employeeView->horizontalModel->setVisible(
employeeModel->rowCount() > 0);
}
```

Whenever the current department changes (including at startup), this slot is called. If there is a valid current department, the function retrieves the department's ID and sets a filter on the employee model. This constrains the employees to those with a matching department ID foreign key. (A filter is just a WHERE clause without the WHERE keyword.) We also update the label that is shown above the employee to show the name of the department employees are in.

If there is no valid department (e.g., if the database is empty), we set the filter to match a non-existent department ID to ensure no records match.

We then call select() on the model to apply the filter. In turn we will emit signals that the view will respond by updating itself. Finally, we show or hide the employee's column headers depending on whether or not any employees are shown.

```
void MainForm::addDepartment()
{
    int row = departmentModel->rowCount();
    departmentModel->insertRow(row);
    QModelIndex index = departmentModel->index(row, Department_Name);
    departmentView->setCurrentIndex(index);
    departmentView->edit(index);
}
```

If the user clicks the Add Dept. button, we insert a new row at the end of the department table, make this row current, and initiate editing of the department name column as though the user had pressed F2 or double-clicked it. If we needed to provide some default values, we would do so by calling insertRow() call.

We have not to concern ourselves with creating unique keys for new records because we have used an auto-incrementing column to handle this for us. If this approach is not possible or suitable, we connect to the model's beforeInsert() signal. This is emitted after the user's edits, just before the insertion takes place in the database. There are similar beforeDelete() and beforeUpdate()