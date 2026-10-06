# LISTING 4-7 SQL Entity provider

```
#if INTERACTIVE
#r "System.Data"
#r "System.Data.Entity"
#r "System.Data.Linq"
#r "FSharp.Data.TypeProviders"
#endif
```

open System.Data
open System.Data.Entity
open Microsoft.FSharp.Data.TypeProviders

// You can use Server Explorer to build your ConnectionString.

```
type internal SqlConnection =
    Microsoft.FSharp.Data.TypeProviders.SqlEntityConnection.ConnectionString =
    @"Data Source=(LocalDB)\v11.0;Initial Catalog=tempdb;Integrated Security=True"
```

```
let internal db = SqlConnection.GetDataContext()
```

> Note Because the SQL Entity type provider cannot be used across assemblies, its type can be only private or internal. This restriction prevents an F# assembly from exposing the type provider to a C# project.

The Entity Framework does not require the database to be SQL Server database. You can use SQL Entity type provider to target an Azure cloud database, as shown in Listing 4-8.

# LISTING 4-8 Using the SQL Entity type provider to connect to an Azure cloud database

```
module SQLEntityConnection

#if INTERACTIVE
#r "System.Data"
#r "System.Data.Entity"
#r "FSharp.Data.TypeProviders"
#endif
```

open System.Data
open System.Data.Entity
open Microsoft.FSharp.Data.TypeProviders

```
<Literal>
let con = ""Server=tcp:<your server>.database.windows.net,1433;
Database=<your database>;User ID=<user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30""
```

172 PART II F#'s Unique Features