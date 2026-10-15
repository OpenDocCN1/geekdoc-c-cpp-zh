# Using DataReader Work with Databases

You can retrieve the data in Windows application by using DataReader instead of DataAdapter. You can use the ExecuteReader to retrieve the rows from a data source. The Read() method of DataReader is used to obtain a row from the data source. There are different DataReaders for different data sources. For example, OleDbDataReader provides a way of reading forward only stream of data rows from OLE DB data provider. The SqlDataReader provides a way of reading forward only stream of data rows from an SQL Server data source. Let's create an application, named UsingDataReader (available in the CD-ROM), in which you can retrieve data from a data source using DataReader. For this, you first need to add Button, Label, TextBox, and ListBox controls to Form1. After adding the controls to Form1, change the text property of the Label control to Enter Text to Find, and the text property of the Button control to FIND.

Now, add the code, shown in Listing 24.11, on the Click event of the Button control:

# Listing 24.11: Showing Code for the Click Event of the Button Control

```
private void button1_Click(object sender, EventArgs e)
{
    SqlDataReader rdr = null;
    SqlConnection con = null;
    SqlCommand cmd = null;
    try
    {
        string ConnectionString = "Data Source=umar-pc;Initial Catalog=Northwind;Integrated Security=True";
        con = new SqlConnection(ConnectionString);
        con.Open();
        string CommandText = "SELECT FirstName, LastName" + " FROM Employees" + " WHERE (LastName LIKE @Find)";
        cmd = new SqlCommand(CommandText);
        cmd.Connection = con;
        cmd.Parameters.Add(new SqlParameter("@Find", System.Data.SqlDbType.Nvarchar, 20, "LastName"));
        cmd.Parameters["@Find"].Value = textBox1.Text;
        rdr = cmd.ExecuteReader();
        listBox1.Items.Clear();
        while (rdr.Read())
        {
            listBox1.Items.Add(rdr["FirstName"].ToString() + " " + rdr["LastName"].ToString());
        }
    }
    catch (Exception ex)
    {
        MessageBox.Show(ex.Message);
    }
    finally
    {
        if (rdr != null)
            rdr.Close();
        if (con.State == ConnectionState.Open)
            con.Close();
    }
}
```

NOTE
You need to modify the value of the ConnectionString property according to your computer configuration. You need to add the System.Data.SqlClient namespace in the Form1.cs file.