# Figure 12-33: Code to filter employee records using a last name

```
37    private void btnFilterByLastName_Click(object sender, EventArgs e)
38    {
39        employeeBindingSource.Filter = "LastName = '" + txtLastName.Text + "'";
40        // Or, use the wild card character "*" for to specify incomplete strings
41        employeeBindingSource.Filter = "LastName LIKE '" + txtLastName.Text + "*'";
42    }
```

Step 2-10: Run the form. Enter the name Hope into the TextBox and click the button. As the navigation bar shows (1 of 2), only the two records with the last name Hope are available on the form.

Next, enter “M” to display all employees whose last name starts with “M.” Verify the result.

# Filtering Records Using the Last Name Selected from a ComboBox

Rather than typing the last name into a TextBox, it would be easier to select a last name from a list of all valid unique last names. You could display all last names in the ComboBox by setting the Data Source to employeeBindingSource and Display Member to LastName. However, this would display the same last name multiple times if there are multiple records with that last name. So, we will create a new data table called LastNames that contains only unique last names, no duplicate names.

# Adding a New Data Table and Corresponding Table Adapter

To add a new data table in the DataSet window, you go through many of the same steps you followed when you added the data source. Creating a data table also creates the table adapter for the table.

Step 2-11: Open the DataSet window by double clicking on the file HRDataSet.xsd in Solution Explorer. You will see the Employee data table and its table adapter.

Step 2-12: Right click anywhere in the window and select Add, TableAdapter (not Data Table). You will be asked to choose the connection. Because you are using the same connection, click Next. You will be asked to choose the Command Type.

Step 2-13: Keep the default, Use SQL Statements. Click Next. You will be asked to enter a SQL statement.

Step 2-14: Click Query Builder instead of typing in the query. Select Employee table from the Add Table window and click Add. Close Add Table window.

Step 2-15: Check LastName field, and click OK. You will see the following SQL to select last names:

```
SELECT    LastName
FROM      Employee
```

Step 2-16: Change the SQL by inserting the key word DISTINCT before LastName, as follows:

```
SELECT    DISTINCT LastName
FROM      Employee
```

Step 2-17: Click Advanced Options. Uncheck the CheckBox for Insert, Update and Delete statements because the Last Names data table is used only for displaying data. Click OK.

Step 2-18: Make sure that Fill a Data Table is checked. Click Next. Click Finish. You will see the new data table with the name DataTable1.