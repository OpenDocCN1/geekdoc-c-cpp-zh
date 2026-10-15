object. The data provider for SQL Server includes the SqlCommand object. The data provider for Oracle includes the OracleCommand object. Let’s create an application, named CommandObject (available in the CD-ROM), to demonstrate the use of Command Object. In this application, we use the SqlCommand object to create a command object. For this, you first need to add a label, named label1 and a combo box, named combobox1 on the Form1. After that, you need to change the Text property of the Label control to Select Employee ID. We display the EmployeeID from the Employees table of the Northwind database in the combobox1 control. After adding the controls to your form, add the code, shown in Listing 24.5, on the Load event of Form1 in the Form1.cs file:

# Listing 24.5: Showing the Code for the Load Event of the Form1

```
private void Form1_Load(object sender, EventArgs e)
{
    SqlConnection connection = new SqlConnection();
    connection.ConnectionString = "Data Source=umar-pc;Initial Catalog=Northwind;Integrated Security=True";
    connection.Open();
    SqlCommand cmd = new SqlCommand("select * from Employees", connection);
    SqlDataAdapter adp = new SqlDataAdapter(cmd);
    DataSet ds = new DataSet();
    adp.Fill(ds, "Employees");
    comboBox1.DataSource = ds.Tables["Employees"];
    comboBox1.DisplayMember = "EmployeeID";
    comboBox1.ValueMember = "EmployeeID";
}
```

# NOTE

> You need to modify the value of the ConnectionString property according to your computer configuration. You need to add the System.Data.SqlClient namespace in the Form1.cs file.

When you execute the code by pressing the F5 key, you would find that combobox1 has values in it. These values are the EmployeeID field values of the Employee table. The output of the code in Listing 24.5 is shown in Figure 24.45:

![](bbox=[0.345, 0.545, 0.67, 0.735])

# Figure 24.45: Retrieving Data in the Combo Box using the Command Object

# Working with DataAdapters

DataAdapters are a set of objects used to exchange data between a data source and DataSet. This means that DataAdapter is responsible for reading data from a database into a DataSet and writing the changed data from the DataSet to the database. The available DataAdapters in a .NET Framework are as follows:

+   - OleDbDataAdapter — Allows you to work with any data source exposed by the OLE DB provider
+   - SqlDataAdapter — Works only with SQL Server
+   - OdbcDataAdapter — Allows you to access an ODBC data source
+   - OracleDataAdapter — Works with Oracle database