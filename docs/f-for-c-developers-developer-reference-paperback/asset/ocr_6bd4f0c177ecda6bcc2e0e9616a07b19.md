Note IntelliSense shows up only within an F# project. When referenced from a C# project, the provided type and the db variable are visible but no column names are shown. This is also true for other type providers. IntelliSense information is provided only by the F# language service.

The stored procedure is common in SQL databases. By default, the LINQ-to-SQL type provider allows stored procedures to also be visible. You can set the storedProcedures parameter to false to disable it, as shown in Listing 4-4.

# LISTING 4-4 Disabling a stored procedure

```
type SqlConnection = Microsoft.CSharp.Data.TypeProviders.SqlDataConnection<ConnectionString>
 = @"DataSource=local;Initial Catalog=TestDatabase;Integrated Security=True"
StoredProcedures=false
let db = SqlConnection.GetData()
```

The SqlConnection also contains a class definition representing tables. The generated table is nested under SqlConnection.ServiceTypes. These types make it possible for you to delete, insert, or update records in a database, as shown in Listing 4-5.

# LISTING 4-5 Updating a database

```
Add a new item
let newRecord = new SqlConnection.ServiceTypes.Course(CourseName = "aa", CourseID = 100)
db.Course.InsertOnSubmit(newRecord)
```

```
try
    db.DataContext.SubmitChanges()
    printf "record added"
with _ -> printf "update failed"

Delete an item
db.Course.DeleteOnSubmit(newRecord)

try
    db.DataContext.SubmitChanges()
    printf "record deleted"
with _ -> printf "update failed"
```

More generally, you can execute any SQL command by using the SqlCommand method in the DataContext. See Listing 4-6.