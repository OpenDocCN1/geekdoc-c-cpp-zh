```
```csharp
catch (System.Exception exc)
{
    this.lblErrorMsg.Text = exc.Message;
}

private void btnLoad_Click_1(object sender,
                              System.EventArgs e)
{
    try
    {
        sConnection =
            "Provider=Microsoft.ACE.OLEDB.12.0;" +
            "Data Source=member.accdb";
        dbConn = new OleDbConnection(sConnection);

        sql = "SELECT * FROM memberTable ORDER " +
              "BY LastName ASC, FirstName ASC;";
        dbCmd = new OleDbCommand();
        dbCmd.CommandText = sql;
        dbCmd.Connection = dbConn;

        memberDataAdap = new OleDbDataAdapter();
        memberDataAdap.SelectCommand = dbCmd;
        memberDS = new DataSet();
        memberDataAdap.Fill(memberDS, "memberTable");
        this.dataGrid1.SetDataBinding
            (memberDS, "memberTable");
    }
    catch (System.Exception exc)
    {
        this.lblErrorMsg.Text = exc.Message;
    }
}
```
```

Exception-handling techniques were included in Example 14-21. As with previous examples presented in this chapter, a blank label object was placed on the form to display error messages.

![](bbox=[0.1728, 0.787, 0.2367, 0.8378])

Notice how there are no calls to the Open( ) or Close( ) methods. When needed, the Fill( ) and Update( ) methods implicitly open the connection that the DataAdapter is using. These methods also close the connection when they are finished. This simplifies your code.