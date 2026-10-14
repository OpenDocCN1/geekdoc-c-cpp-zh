# Method and properties of the SqlDataSource class for inserting rows

| Method | Description |
|---|---|
| Insert() | Executes the Insert command defined for the data source. |
| Property | Description |
| InsertCommand | The Insert command to be executed. |
| InsertParameters["name"] | The parameter with the specified name. |

# Property of the Parameter class for inserting rows

| Property | Description |
|---|---|
| DefaultValue | The default value of a parameter. This value is used if no other value is assigned to the parameter. |

# Code that uses a SqlDataSource control to insert a row

```
protected void btnAdd_Click(object sender, EventArgs e)
{
    SqlDataSource1.InsertParameters["CategoryID"].DefaultValue
        = txtID.Text;
    SqlDataSource1.InsertParameters["ShortName"].DefaultValue
        = txtShortName.Text;
    SqlDataSource1.InsertParameters["LongName"].DefaultValue
        = txtLongName.Text;
    try
    {
        SqlDataSource1.Insert();
        txtID.Text = "";
        txtShortName.Text = "";
        txtLongName.Text = "";
    }
    catch (Exception ex)
    {
        lblError.Text = "A database error has occurred. " +
            "Message: " + ex.Message;
    }
}
```

# Description

+   - The GridView control doesn’t support insert operations, but you can use the GridView’s data source to insert rows into the database. When you do, the new row will automatically be shown in the GridView control.
+   - To provide for inserts, the page should include controls such as text boxes for the user to enter data and a button that the user can click to insert the data.
+   - To use a SqlDataSource control to insert a database row, first set the DefaultValue property of each insert parameter to the value you want to insert. Then, call the Insert method.
+   - The Insert method may throw a SqlException if a SQL error occurs. The most likely cause of the exception is a primary key constraint violation.

Figure 14-11   How to insert a row in a GridView control