Handling Events | 563

10. Click the Genres item in the Management menu and deleting the Rap and Hip-Hop genre. This time the genre is successfully deleted from the database.

11. To see the error you would get without this error handling, comment out the line in the Code Behind that sets ExceptionHandled to True. Save your changes, open the page again in your browser, and try to delete genre reviews. You will get a detailed ASP.NET error instead, shown in Figure 15-12.

Server Error in '/' Application.

The DELETE statement conflicted with the REFERENCE constraint "FK_Review_Genre". The conflict occurred in database "C:\BEGASPN1\SITE\APP_DATA\PLANETWROX.MDF", table "dbo.Review", column 'Gnerld'.
The statement has been terminated.

FIGURE 15-12

Notice how this error is almost identical to the one you got near the end of Chapter 12 when you tried to delete a genre manually. Do not forget to enable both lines you commented out in this exercise when you're done, so links are disabled when you still get a friendly error message when the genre can't be deleted.

# How It Works

When you click the Delete link in the GridView visible in Figure 15-11, the GridView triggers the Delete command on the associated SqlCommand control. As you have seen in previous chapters, this control tries to send a DELETE statement to the database. The database tries to delete the requested genre from the database, but finds out that it cannot because the genre has related reviews. This results in a foreign key constraint error, which means the genre cannot be deleted because its ID is used as a foreign key in another table.

This foreign key constraint error is returned from the database and eventually ends up in the Exception property of the e of the SqlDataSource1_Deleted handler. The code checks if there was an error (e.Exception is not Nothing/null) and checks the type of the exception to find out it's a SqlException:

# VB.NET

```
If e.Exception Is Not NothingAndAlso
    TypeOf(e.Exception) Is SqlException Then
```

```
End If
```

# C#

```
if (e.Exception != null && e.Exception is SqlException)
{
}
```

When you are working with a SQL Server database, as is the case in the Planet Wrox example, the errors thrown by the database are of type SqlException from the System.Data.SqlClient namespace you imported in this exercise. This enables you to clearly separate database errors from other errors.