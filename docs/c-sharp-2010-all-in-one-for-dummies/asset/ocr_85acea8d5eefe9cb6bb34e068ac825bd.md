```
private void Form1_Load(object sender, EventArgs e)
{
    // TODO: This line of code loads data into the 'assets_MaintenanceDataSet.Part_Faults' table. You can move, or remove it, as needed.
    this.part_FaultsTableAdapter.Fill(this.assets_MaintenanceDataSet.Part_Faults);
    // TODO: This line of code loads data into the 'assets_MaintenanceDataSet.Parts' table. You can move, or remove it, as needed.
    this.partsTableAdapter.Fill(this.assets_MaintenanceDataSet.Parts);
}
```

While this is fairly straightforward, it obviously isn't everything that you need. The rest of the code is in the file that generates the visual form itself, supporting the visual components.

The time may come when you want to connect to a database without using visual tools. I discuss the steps in the earlier section "How the Data Classes Fit into the Framework," and here I show the code to go with it:

+   1. SqlConnection mainConnection = new SqlConnection();
+   2. mainConnection.ConnectionString = "server={local};database=Assets_Maintenance;Trusted_Connection=True"
+   3. SqlDataAdapter partsAdapter = new SqlDataAdapter("SELECT * FROM Parts", mainConnection)
+   4. DataSet partsDataSet = new DataSet();
+   5. mainConnection.Open();
+   6. partsAdapter.Fill(partsDataSet);
+   7. mainConnection.Close();

![](bbox=[0.12, 0.7, 0.22, 0.85])

This becomes useful especially when you want to build a Web service or a class library — though it should be noted that you can still use the visual tools in those project types.

Let's talk about this a line at a time. Line one sets up a new data connection, and line two populates it with the connection string. You can get this from your DBA or from the properties panel for the data connection.

Line three has a SQL Query in it. In Chapter 1, I talk about how this is a bad deal, and you should use Stored Procedures. That's true. Don't use inline SQL for production systems. I could have just as easily put a stored procedure name in there.

Line four builds a new dataset. This is where the schema of the returned data is held and what I would use to navigate the data.