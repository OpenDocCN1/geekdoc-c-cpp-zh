9 Import the System.Data.SqlClient namespace into the DatabaseOperationsExample application by using the using statement as shown in the following code snippet:

```
using System.Data.SqlClient;
```

10 Add the highlighted code given in Listing 8.2 in the Load event of the Form1 form to display employee details on a DataGridView control:

# Listing 8.2: Populating the Dataset

```
private void Form1_Load(object sender, EventArgs e)
{
    sqlDataAdapter1.Fill(dataSet11);
}
```

Listing 8.2 shows that the Fill() method is used to populate the dataSet11 dataset with employees details.

11 Press the F5 key from the keyboard to execute the DatabaseOperationsExample application. The output appears, as shown in Fig.C8-8.25:

![](bbox=[0.13, 0.5, 0.85, 0.62])

Fig.C8-8.25

As shown in Fig.C8-8.25, the Fill() method of the SqlDataAdapter class is used to populate the DataSet object, dataSet1 with data from the NORTHWND table of SQL Server.

Next, let’s learn about the different types of data binding in Windows Forms.

# Types of Data Binding in Windows Forms

Data binding refers to the binding of controls to a data from a data source to display the data. In traditional data binding, the data binding operations were mainly performed on data stored in databases. However, with Windows Forms data binding, you can now bind data from SQL Server databases and other structures, such as collections and arrays.

You can perform data binding by using a SQL Server database by binding either a particular field in a table or by binding the entire table to a control. For example, you can bind a text box to the ProductName field of a table or bind the entire table to a DataGridView control.

# Simple Data Binding Using BindingContext Class