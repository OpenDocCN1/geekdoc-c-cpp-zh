# ASP.NET Web Services

| WebServiceUpDtP | SQLUpdateSP() |
| --- | --- |
| A | using System.Configuration;
using System.Data;
using System.Data.SqlClient;
using System.Web.Services; | |
| B | public SQLBase SQLUpdateSP(string stringName, float GPA, int Credits, string Major, string SchoolYear, string byte[], string image, string StudentID) | |

```
[WebMethod]
public SQLBase SQLUpdateSP(string stringName, float GPA, int Credits, string Major, string SchoolYear, string byte[], string image, string StudentID)
{
    string cmd = "dbo.WebUpdateDataSet";
    SqlConnection connection = new SqlConnection();
    SQLBase Result = new SQLBase();
    SqlCommand command = new SqlCommand(cmd);
    int intUpdate;
    Result.SQLOK = true;
    connection.Open();
    if (connection == null)
    {
        Result.Error = "Database connection is failed";
        ReportError(Result);
        return null;
    }
    command.Connection = connection;
    command.CommandType = CommandType.StoredProcedure;
    command.CommandText = cmd;
    command.Parameters.Add(\@Name", SqlDbType.VarChar).Value = stringName;
    command.Parameters.Add(\@GPA", SqlDbType.Char).Value = GPA;
    command.Parameters.Add(\@Major", SqlDbType.Text).Value = Major;
    command.Parameters.Add(\@SchoolYear", SqlDbType.Text).Value = SchoolYear;
    command.Parameters.Add(\@Credits", SqlDbType.Int).Value = Credits;
    command.Parameters.Add(\@Email", SqlDbType.Text).Value = Email;
    command.Parameters.Add(\@image", SqlDbType.Image).Value = image;
    command.Parameters.Add(\@StudentID", SqlDbType.Text).Value = StudentID;
    intUpdate = command.ExecuteNonQuery();
    command.Dispose();
    connection.Close();
    if (intUpdate == 0)
    {
        Result.Error = "Data updating is failed";
        ReportError(Result);
    }
    return Result;
}
```

FIGURE 9.97 The codes for the type of argument passed into this method to SQLUpdateSP().

The only modifications are to change the type of argument passed into this method to SQLBase since we only need to check the status of this data updating action, and change the member data of the base class to SQLOK.

Go to File | Save All item to save these modifications. Next let's use our method SQLDeleteSP() to call a stored procedure to delete a student record.

# 9.5.4 Create a Web Method To Call Stored Procedure To Delete Student Records

As discussed in Section 7.1.1 in Chapter 7, to delete a record from a relational database, one needs to follow the operational steps listed below:

+   1) Delete records that are related to the parent table with the foreign keys from children tables.
2) Delete records that are defined as primary keys from the parent table.