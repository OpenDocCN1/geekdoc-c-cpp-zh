
**Figure 12-33: Code to filter employee records using a last name**

```
37    private void btnFilterByLastName_Click(object sender, EventArgs e)
38    {
39        employeeBindingSource.Filter = "LastName = '" + txtLastName.Text + "'";
40        // Or, use the wildcard character "*" to specify incomplete strings
41        employeeBindingSource.Filter = "LastName LIKE '" + txtLastName.Text + "*'";
42    }
```

Step 2-10: Run the form. Enter the name Hope into the TextBox and click the button. As the navigation bar shows (1 of 2), only the two records with the last name Hope are available on the form.

Next, enter “M” to display all employees whose last name starts with “M.” Verify the result.

## Filtering Records Using the Last Name Selected from a ComboBox

Rather than typing the last name into a TextBox, it would be easier to select a last name from a list of all valid unique last names. You could display all last names in the ComboBox by setting the Data Source to employeeBindingSource and Display Member to LastName. However, this would display the same last name multiple times if there are multiple records with that last name. So, we will create a new data table called LastNames that contains only unique last names, no duplicate names.

### Adding a New Data Table and Corresponding Table Adapter

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

**Figure 12-37: Code to filter employee records**

```
44  private void cboLastNames_SelectionChangeCommitted(object sender, EventArgs e)
45  {
46      employeeBindingSource.Filter = "LastName = '" + cboLastNames.SelectedValue + "'";
47  }
```

Note that you should use the SelectedValue (not the Text property) of the ComboBox, which gives the value of the field specified by the ValueMember property. The Text property is not changed at the time this event is raised, because this event is raised before the SelectedIndexChanged event; so, you cannot use the Text property in this event handler.

Step 2-24: Create the SelectionChangeCommitted event handler for cboLastNames, and add the code from Figure 12-37. Run the form and test the code.

### Cancelling a Filter

To cancel a filter specified using the BindingSource.Filter property, set the Filter to a null string.

Step 2-25: Add a button named btnCancelFilter, and add the code from Figure 12-38 to the Click event handler. Run the form and test the code.

**Figure 12-38: Code to cancel filter**

```
48
49  private void btnCancelFilter_Click(object sender, EventArgs e)
50  {
51      employeeBindingSource.Filter = "";
52  }
```

It’s time to practice! Do Exercise 12-2

## Selecting a List from One Table to Filter Another Table

Suppose you want to select a department number from a ComboBox and filter employee records to view only employees from that department. The HR database includes a second table named department, as shown in Figure 12-39.

**Figure 12-39: Department table**

| DeptNo | DeptName | DeptPhone |
|---|---|---|
| 1 | Accounting | 920-424-1414 |
| 2 | Finance | 920-424-3377 |
| 3 | Marketing | 920-424-2442 |
| 4 | Purchasing | 920-424-0405 |
| 5 | Human Resources | 920-424-1166 |
| 6 | Information Technology | 920-424-3020 |

A list of unique department numbers for display in the ComboBox can be obtained from the Employee table by altering the SQL, or it can be obtained from the Department table. Because the Employee table is significantly larger than the Department table, it would be more efficient to get such a list from the Department table. Getting department numbers from the Department table also gives you the option to display department names in the ComboBox but use department numbers to filter records.

To get the department numbers (and names, if needed), you need to first create a data table and table adapter for Department table using the same steps that you followed to create the LastNames data table.

It’s time to practice! Do Exercise 12-3.

### Review Question

12.9 The data from a table named Employee is displayed on a form in Details View in TextBoxes. The controls on the form were created by dragging and dropping the data table on the form.

What would be the effect of executing the following statement on the set of records that the user can see on the form?

```
employeeBindingSource.Filter = "CountryId = 22";
```

What would be the effect of executing the above statement on the records stored in the Employee data table in memory?

## 12.8 Selecting Records Using the Table Adapter

In the previous section, you selected records using the Filter property of the binding source that controls what is transferred between a data table and the form. Another way to select records is to use the table adapter to change the SQL language that it uses to transfer data from the database to the dataset. This is fundamentally different from using the binding source.

### Binding Source versus Table Adapter to Select Records

When you use binding source to filter records, typically the entire data from a table(s) is loaded from the database into a data table in memory. The binding source is used to help the user select different groups of data to work with. After the data are loaded into the data table, any change made to the database is not reflected in the data that the user sees. So, the user may not be seeing the latest data. Further, large tables consume a large amount of memory. A benefit of loading the entire table into memory and then filtering records using the binding source is that the database needs to be accessed only once in the beginning, thus reducing the network traffic.

When you use the table adapter, every time the user wants a group of data, it is loaded from the database into a data table and displayed on a form. So, each time a group of data is loaded, it will include the latest changes. The memory usage is lower because only selected records are held in data tables. This also means that the database is accessed every time the user requests a group of records.

Next, we look at the use of the table adapter to select records.

Step 3-5: Comment out the statement in the Load event handler, which uses the standard Fill method, as shown in Figure 12-42. Add the code from Figure 12-42 to the Click event handler of the button.

**Figure 12-42: Load event handler for the EmployeeSearch_ParmQry form**

```
28  private void EmployeeSearch_ParmQry_Load(object sender, EventArgs e)
29  {
30      // TODO: This line of code loads data into the 'hRDataSet.Employee' table.
31      //this.employeeTableAdapter.Fill(this.hRDataSet.Employee);
32  }
33  private void btnSelectRecords_Click(object sender, EventArgs e)
34  {
35      employeeTableAdapter.FillByLastName(hRDataSet.Employee, txtLastName.Text);
36  }
```

Step 3-6: Run the form and test the code.

Step 3-7: To give the user an option to display all records, add a button, btnAllRecords, with the caption “Display All.” Add the code to use the standard query, shown in Figure 12-43. Run the form and test the code.

**Figure 12-43: Standard Fill method to display all records**

```
37
38  private void btnAllRecords_Click(object sender, EventArgs e)
39  {
40      this.employeeTableAdapter.Fill(this.hRDataSet.Employee);
41  }
```

It’s time to practice! Do Exercise 12-4.

### Review Question

12.10 The data from a table named Employee are displayed on a form in Details View in TextBoxes. The controls on the form were created by dragging and dropping the data table on the form. A parameter query named FillByLastName was created using the following SQL:

```
SELECT EmpId, LastName, FirstName, DateOfBirth, Phone, DeptNo, CountryId, Salary, FullTime
FROM dbo.Employee
WHERE DeptNo = @DeptNo
```

What would be the effect of executing the following statement on the Employee data table? `employeeTableAdapter.FillByLastName(hRDataSet.Employee, 11)`
