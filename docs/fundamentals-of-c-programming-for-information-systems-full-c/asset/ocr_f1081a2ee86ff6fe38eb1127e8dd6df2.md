# Chapter 12

11.2 Hiding a form keeps the form and its properties and settings in memory. You don’t lose the data entered/displayed in controls at runtime.
Closing a form removes the form from memory. So, you lose all current settings and data.

11.3 The Show method opens the form and C# continues processing the statements that follow the statement. However, with the ShowDialog method, C# opens the form and stops processing the statements that follow the statement until the dialog window is closed.

11.4 .Create a Public method within a class and call it from different forms.

11.5 A static method is not associated with a specific instance (object) of the class that contains the method. It is associated only with the class. So, it is invoked using the class name.
To call a nonstatic method, you have to create an object of the class and use the object name in place of the class name.

11.6 A context menu is associated with a control, and it is displayed by right clicking the control.

11.7 Option 3: Selecting an item from a Context menu

12.1 data tables are temporary tables maintained in memory. Each data table may contain data from one or more database tables that are typically stored on the disk.

12.2 The table adapter connects the data table to the database, and retrieves data from and saves data to the database.

12.3 The binding source links the user interface controls on the form to a data table.

12.4 The Fill method of the table adapter copies data from the database table into the data table.

12.5 The Update method of the table adapter saves the data from the data table into the database table

12.6 A data bound control is a user interface control that is linked to a data source

12.7 The data in a data bound control is linked to the binding source, and the binding source is linked to the data table.

12.8 Set all DataBindings to None.
Set DataSource to CustomerBindingSource
Set DisplayMember to CustomerId

12.9 The user will be able to see only employee records with CountryId, 22.
It will have no effect on the records in the data table. The data table still will have all records from Employee table.

12.10 The Employee data table will have only records for employees from DeptNo 11.

12.11 Connection string, SQL