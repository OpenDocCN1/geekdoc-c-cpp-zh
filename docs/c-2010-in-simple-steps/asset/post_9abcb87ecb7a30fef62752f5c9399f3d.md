
10 Click the Query Builder button to create an SQL statement or select an existing stored procedure, to generate an SQL statement.

The Query Builder dialog box appears along with the Add Table dialog box (Fig.C#8.13).

11 Select a table from the Add Table dialog box. In our case, we select the Employees table (Fig.C#8.13).

12 Click the Add button to add the Employees table to the Query Builder dialog box (Fig.C#8.13).

13 Click the Close button to close the Add Table dialog box, as shown in Fig.C#8.13:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_273_0.png)

Fig.C#8.13

The Employees table is added to the Query Builder dialog box (Fig.C#8.14).

At the top of the Query Builder dialog box, you can see all the fields of the Employees table; you can select the fields from the table as per your choice.

14 Select the check box beside the *(All Columns) option from the Employees table (Fig.C#8.14).

15 Click the OK button to create the SQL statement, as shown in Fig.C#8.14:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_273_1.png)

Fig.C#8.14

The SQL statement appears in **Data Adapter Configuration Wizard** page (Fig.C#8.15).

- 16. Click the **Next** button, as shown in Fig.C#8.15:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_274_0.png)

Fig.C#8.15

The Data Adapter Configuration Wizard page appears with the information of a successful configuration of the data adapter.

- 17. Click the **Finish** button to close the **Data Adapter Configuration Wizard** page.

The sqlDataAdapter1 data adapter and the sqlConnection1 connection object appear on the component tray, as shown in Fig.C#8.16:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_274_1.png)

Fig.C#8.16

- 18. Select **Data→Preview Data** from the menu bar to preview the data from the data adapter, as shown in Fig.C#8.17:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_274_2.png)

Fig.C#8.17

The Preview Data dialog box appears (Fig.C#8.18).

- 19. Click the Preview button to view the data from the database in the Results pane (Fig.C#8.18).
- 20. Click the Close button to close the Preview Data dialog box, as shown in Fig.C#8.18:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_275_0.png)

Next, let's learn to display data from a data source in a Windows Forms application by using a dataset.

## Creating a Dataset

Datasets, as already explained, contains a cached copy of the tables of a database. A dataset is independent of the database and so the interaction with existing databases is controlled through the data adapter. You can fill data in a dataset by using the Fill() method of the data adapter.

Now, let's perform the following steps to create a dataset:

- 1. Open the DatabaseOperationsExample application.
- 2. Select Data→Generate Dataset from the menu bar, as shown in Fig.C#8.19:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_275_1.png)

The Generate Dataset dialog box appears, prompting you to select a dataset (Fig.C#8.20).

You can select an existing dataset or create a new one. By default, the New radio button is selected. You can provide a name for the new dataset or use the existing default name as DataSet1. The Generate Dataset dialog box also prompts you to select a table to add to the dataset. In the Generate Dataset dialog box, you can provide a name for the dataset object and select the table(s) that you want to add to the dataset object. In our case, we have retained the default settings (Fig.C#8.20).

- 3. Click the OK button to add the dataset to the DatabaseOperationsExample application, as shown in Fig.C#8.20:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_276_0.png)

Fig.C#8.20

The dataset, dataSet1, is added to the component tray, as shown in Fig.C#8.21:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_276_1.png)

Fig.C#8.21

After creating a dataset, let's learn how to use a data adapter to retrieve data into a dataset.

## Using a Data Adapter to Retrieve Data into a Dataset

So far, we have created a data adapter and a dataset. Let's now see how to display data on a DataGridView control by using a data adapter and dataset. For this, perform the following steps:

- 1. Open the DatabaseOperationsExample application.
- 2. Drag a DataGridView control from the Data tab of Toolbox and drop it into the Form1 form. A smart tag automatically appears along with the DataGridView control that you add.
- 3. Click the Choose Data Source drop-down list to view a list of all the available data sources (Fig.C#8.22).
- 4. Click the triangle glyph in front of the Other Data Sources option to expand it (Fig.C#8.22).
- 5. Click the triangle glyph in front of the Project Data Sources option to expand it (Fig.C#8.22).
- 6. Select the DataSet1 data source, as shown in Fig.C#8.22:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_277_0.png)

**Fig.C#8.22**

The **dataSet1BindingSource** binding source is added to the component tray (Fig.C#8.23). A binding source refers to the data source from where you can obtain data. In this case, the data is obtained by using a dataset.

- 7. Click the **Choose Data Source** down arrow and select the **Employees** table from the drop-down list that appears, as shown in Fig.C#8.23:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_277_1.png)

**Fig.C#8.23**

The **employeesBindingSource** binding source is added to the component tray, as shown in Fig.C#8.24:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_277_2.png)

**Fig.C#8.24**

- 8. Resize the form (**Basic Database Operations**) to accommodate the data of the **Employees** table.

9 Import the System.Data.SqlClient namespace into the DatabaseOperationsExample application by using the using statement as shown in the following code snippet:

```
using System.Data.SqlClient;
```

10 Add the highlighted code given in Listing 8.2 in the Load event of the Form1 form to display employee details on a DataGridView control:

### Listing 8.2: Populating the Dataset

```
private void Form1_Load(object sender, EventArgs e)
{
    sqlDataAdapter1.Fill(dataSet1);
}
```

Listing 8.2 shows that the Fill() method is used to populate the dataSet1 dataset with employees details.

11 Press the F5 key from the keyboard to execute the DatabaseOperationsExample application. The output appears, as shown in Fig.C#8.25:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_278_0.png)

Fig.C#8.25

As shown in Fig.C#8.25, the Fill() method of the SqlDataAdapter class is used to populate the DataSet object, dataSet1 with data from the NORTHWND table of SQL Server.

Next, let’s learn about the different types of data binding in Windows Forms.

## Types of Data Binding in Windows Forms

Data binding refers to the binding of controls to a data from a data source to display the data. In traditional data binding, the data binding operations were mainly performed on data stored in databases. However, with Windows Forms data binding, you can now bind data from SQL Server databases and other structures, such as collections and arrays.

You can perform data binding by using a SQL Server database by binding either a particular field in a table or by binding the entire table to a control. For example, you can bind a text box to the ProductName field of a table or bind the entire table to a DataGridView control.

### Simple Data Binding Using BindingContext Class

In simple terms, you can say that simple data binding is the ability of a control to bind a single data element.

Performing the following steps to illustrate simple data binding:

- 1. **Create** an application named **WindowsFormsDataBinding**.
- 2. **Set** the **Text** property of **Form1** to **Simple Data Binding**.
- 3. **Drag** and drop the following controls on **Form1** and set the values for their properties, as shown in Table 8.3:
- 4. **Import** the **System.Data.SqlClient** namespace in the code-behind file of the **WindowsFormsDataBinding** application by using the using statement, as shown in the following code snippet:
- 5. **Add** the highlighted code given in Listing 8.3 in the **Load** event of the **Form1** form to display the details of the employee whose **EmployeeID** is 6:
- 6. **Press** the **F5** key to execute the **WindowsFormsDataBinding** application. The output appears, as shown in Fig.C#8.26:

### Table 8.3: Controls with their Properties and Values

| Control Name | Property Name | Value |
|---|---|---|
| label1 | Text | Employee ID |
| label2 | Text | First Name |
| label3 | Text | Last Name |
| label4 | Text | Title |
| textBox1 | Enabled | False |
| textBox2 | Enabled | False |
| textBox3 | Enabled | False |
| textBox4 | Enabled | False |

```csharp
using System.Data.SqlClient;
```

### Listing 8.3: Displaying Simple Data Binding

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    SqlConnection con;
    con = new SqlConnection("Data Source=TEMP-PC\\SQLEXPRESS;Initial Catalog=\\SQL SAMPLE DATABASE\\NORTHWND.MDF;Integrated Security=True");
    con.Open();
    DataSet ds = new DataSet();
    SqlDataAdapter da = new SqlDataAdapter("Select * from Employees where EmployeeID=6", con);
    da.Fill(ds,"Employees");
    textBox1.DataBindings.Add("Text", ds, "Employees.EmployeeID");
    textBox2.DataBindings.Add("Text", ds, "Employees.LastName");
    textBox3.DataBindings.Add("Text", ds, "Employees.FirstName");
    textBox4.DataBindings.Add("Text", ds, "Employees.Title");
}
```

In Listing 8.3, the DataBindings property is used to bind text boxes to the Employees table.
