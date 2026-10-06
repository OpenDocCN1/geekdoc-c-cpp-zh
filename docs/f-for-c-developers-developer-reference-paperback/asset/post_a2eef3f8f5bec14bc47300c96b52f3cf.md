
# LISTING 4-7 SQL Entity provider

```sharp
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

```sharp
type internal SqlConnection =
    Microsoft.FSharp.Data.TypeProviders.SqlEntityConnection.ConnectionString =
    @"Data Source=(LocalDB)\v11.0;Initial Catalog=tempdb;Integrated Security=True"
```

```sharp
let internal db = SqlConnection.GetDataContext()
```

Note Because the SQL Entity type provider cannot be used across assemblies, its type can be only private or internal. This restriction prevents an F# assembly from exposing the type provider to a C# project.

The Entity Framework does not require the database to be SQL Server database. You can use SQL Entity type provider to target an Azure cloud database, as shown in Listing 4-8.

# LISTING 4-8 Using the SQL Entity type provider to connect to an Azure cloud database

```fsharp
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

```fsharp
<Literal>
let con = "Server=tcp:<your server>.database.windows.net,1433;
Database=<your database>;User ID=<user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
```

// You can use Server Explorer to build ConnectionString.
type internal SqlConnectionT =
    Microsoft.Fsharp.Data.SqlProviders.SqlEntityConnection<ConnectionString> = con
let internal db = SqlConnectionT.GetDataContext()
```

The way to add and delete commands for the SQL Entity type provider is different; the provider uses AddObject and DeleteObject to add a record or remove records from a database. Listing 4-9 shows how to use these methods.

# LISTING 4-9 Adding and removing records from an Azure cloud database using the SQL Entity type provider

```fsharp
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
password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"

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

# Execution result

1 record(s) affected
1 record(s) affected

If you want to execute your own SQL query, you can use the ExecuteStoreQuery method.
Listing 4-10 shows how to use this method to check the total number of courses in the database.

# LISTING 4-10 Executing your query by using the SQL Entity provider

```fsharp
let result = db.DataContext.ExecuteStoreQuery("select count(*) from Course")
printf("%d course(s) in the database", (result | Seq.head))
```

# SQL Entity Type Provider Parameters

Like the SQL type provider, the SQL entity provider needs either ConnectionString
ConnectionStringName as a parameter. The full list of parameters is shown in Table 4-2.

TABLE 4-2 SQL entity type parameters

| Parameter Name | Description |
|---|---|
| ConfigFile | The name of the configuration file used for connection strings. The default value is either app.config or web.config. |
| ConnectionString | The connection string for the database. |
| ConnectionStringName | The name of the connection string for the database connection in the configuration file. |
| DataDirectory | The name of the data directory, to replace DataDirectory in the connection string. The default is the project folder or script folder. |
| EntityContainer | The name to use for the EntityContainer in the conceptual model. |
| ForceUpdate | Requires a direct connection to the database to be available at design time, and refreshes the refresh of the local schema file. The default value is TRUE. |
| LocalSchemaFile | The local file for the database schema. |
| Pluralize | Automatically pluralizes class and member names using English language rules. The default value is FALSE |
| Provider | The name of the ADO.NET provider to be used for Store Schema Definition (SDL). If you are interested in SSL, please refer to MSDN document at http://msdn.microsoft.com/en-us/data/jj6S2016. The default provider is System.Data.SqlClient |
| ResolutionFolder | The folder used to resolve relative file paths at compile time. The default value is the project folder or script folder. |
| SuppForeignKeyProperties | Excludes foreign keys in entity type definitions. The default value is FALSE. |

# WSDL Type Provider

The web is another area that is rich with data. The public application programming interfaces (APIs) exposed by companies around the world is increasing exponentially year by year. If the data schema can be automatically accessed and shown with IntelliSense, this will make your coding significantly easier and boost productivity.

Web Services Description Language (WSDL) is an XML-based language which is used to describe the functionality provided by a web service. A WSDL file offers a machine-readable XML document that explains how the service can be called, what operations are available, what parameters are required, and the values that can be returned.

The easiest way to add a WSDL type provider is to use the Add New Item dialog box.

![FIGURE 4-8 Using the Add Item dialog box to add a WSDL type provider](img/63aaf94e22830ab98ce5946be8ef194_0.png)

# LISTING 4-11 WSDL type provider

```fsharp
open System.Runtime.Serialization
open System.ServiceModel
open Microsoft.FSharp.Data.TypeProviders

// You can sign up for a Bing developer account
let BING_APP_ID = "your Bing Developer Key"

type RouteService = Microsoft.FSharp.Data.TypeProviders.WsdlService<ServiceUri = "http://dev.virtualearth.net/webservices/v1/routeservice.svc?wsdl">
type RouteCommon = RouteService.ServiceTypes.dev.virtualearth.net.v1.common
type Route = RouteService.ServiceTypes.dev.virtualearth.net.v1.route
```

```fsharp
let startPoint = Route.Waypoint(
    Location = RouteCommon.Location(
        Latitude = 47.64012046, Longitude = -122.1297104))
let endpoint = Route.Waypoint(
    Location = RouteCommon.Location(
        Latitude = 47.62049103, Longitude = -122.3492355))
```

```fsharp
let routReq1 = new Route.Request(Waypoints = [startPoint; endpoint])
routReq1.Credentials <- new RouteCommon.Credentials(ApplicationId = BING_APP_ID)
RouteService.GetBasicHttpBinding().IRouteService().CalculateRoute(routReq1).Result
Summary.Distance | printf "Driving Distance = %A (miles)"
```

Note A Bing maps developer key is required to use IntelliSense and compile the code.
