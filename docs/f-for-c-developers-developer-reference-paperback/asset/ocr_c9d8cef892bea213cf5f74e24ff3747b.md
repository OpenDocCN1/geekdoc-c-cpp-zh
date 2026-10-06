```
// You can use Server Explorer to build ConnectionString.
type internal SqlConnectionT =
Microsoft.Fsharp.Data.SqlProviders.SqlEntityConnection<ConnectionString> = con
let internal db = SqlConnectionT.GetDataContext()
```

The way to add and delete commands for the SQL Entity type provider is different; the provider uses AddObject and DeleteObject to add a record or remove records from a database. Listing 4-9 shows how to use these methods.

# LISTING 4-9 Adding and removing records from an Azure cloud database using the SQL Entity type provider

```
module SqlEntityConnection1

#if INTERACTIVE
#r "System.Data"
#r "System.Data.Entity"
#r "FSharp.Data.TypeProviders"
#endif

open System.Data
open System.Data.Entity
open Microsoft.Fsharp.Data.TypeProviders

[<Literal>]
let con = "tcp:<your server>.database.windows.net,1433;
Database=<your database>;User ID=<user name>;Password=<your
password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30""

// You can use Server Explorer to build ConnectionString.
type internal SqlConnectionT =
Microsoft.Fsharp.Data.SqlProviders.SqlEntityConnection<ConnectionString> = con

let internal db = SqlConnectionT.GetDataContext()

let internal newRecord = new SqlConnectionT.Services.Course(CourseName = "aa",
CourseID = 100)
db.Course.AddObject(newRecord);
try
  let recordNumber = db.DataContext.SaveChanges()
  printfn "%d record(s) affected" recordNumber
with __ -> printf "update failed"
db.Course.DeleteObject(newRecord);
try
  let recordNumber = db.DataContext.SaveChanges()
  printfn "%d record(s) affected" recordNumber
with __ -> printf "update failed"
```