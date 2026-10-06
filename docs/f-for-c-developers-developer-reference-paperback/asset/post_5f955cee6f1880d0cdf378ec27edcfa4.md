
| Parameter Name | Description |
|---|---|
| EnableDataBinding | Indicates whether the INotPropertyChanged interface should be added on all data contract types to enable data binding. The default value is FALSE. |
| ForceUpdate | Requires a direct connection to the service to be available at design time, and forces the refresh of the local schema file. The default value is TRUE. |
| LocalSchemaFile | The wsdl schema file to store locally cached schema. |
| MessageContract | Indicates whether message contract types should be generated. The default value is FALSE. |
| ResolutionFolder | The folder used to resolve relative file paths at compile. The default value is the folder that contains the project or script. |
| Serializable | Indicates whether the generated classes should be marked with the Serializable attribute. The default value is FALSE. |
| ServiceUri | The URI for the WSDL service. This is a mandatory property. |

## OData Type Provider

Another way to access remote services or data is to use the Open Data Protocol (OData) type provider. OData is an open web protocol for querying and updating data over the HTTP transport protocol. You can use it to retrieve results in formats like Atom, JSON, or plain XML. Figure 4-9 shows how to use Visual Studio to create an OData type provider, and the generated sample code is shown in Listing 4-12. The OData type provider does not support fixed queries. How to download the fixed query schema to work with the OData type provider.

![](img/63aaf94e22830ab98ce16c5946be8ef6_196_0.png)

FIGURE 4-9 - Using the New Item dialog box to add an OData type provider

### LISTING 4-12 OData type provider

```fsharp
open System.Data.Services.Client
open Microsoft.Fsharp.Data.TypeProviders

// Access demographic info such as population and income from the OData service at
Azure Marketplace. For more information, go to https://datamarket.azure.com/dataset/
c7514924-7cbac-4ac9-97fb-677317ef656

type Demographics = Microsoft.Fsharp.Data.TypeProviders.ODataService<"https://api.datamarket.azure.com/Esri/KeyUSDemographicsTrial/"> =
let ctx = Demographics.GetDataContext()

// To sign up for an Azure Marketplace account at https://datamarket.azure.com/
account/Infox.Credentials <- System.Net.NetworkCredential("your liveID",
    "your Azure Marketplace Key*")
```

> Note: You need a Windows Live ID and an Azure Marketplace key to show IntelliSense and compile the code from the previous example.

## OData Type Provider Parameters

Compared to the WSDL type provider, the OData type provider’s parameter list (shown in Table 4-4) is much shorter. Like the WSDL type provider, ServiceUri is a mandatory parameter; the other parameters are optional.

### TABLE 4-4 OData type provider parameters

| Parameter Name | Description |
|---|---|
| DataCollection | Indicates whether or not to generate collections derived from DataService. The default value is FALSE. |
| ForceUpdate | Requires a direct connection to the service to be available at design time, and forces the refresh of the local schema file. The default value is TRUE. |
| LocalSchemaFile | The local csdl file for the service schema. |
| ResolutionFolder | The folder used to resolve relative file paths at compile time. The default value is the folder that contains the project or script. |
| ServiceUri | The URI for the OData service. This parameter is mandatory. |

## Other Type Providers

As I mentioned at the beginning of this chapter, the type provider is extensible. Because the type provider concept is public, many type providers have been developed by the community. Many of these type providers are provided by the FSharpX on GitHub. I'm not going to present a detailed introduction to these type providers, but you can find more about them at https://github.com/fsharp/fsharpx. This website provides information on type providers such as:

- **File System**: Used to provide type information from a file system. The type provider provides types for directories and files on the computer.
- **Xml File**: Used to provide type information for an XML file.
- **JSON**: Used to provide type information for JSON.
- **Registry**: Used to provide type information from the registry.
- **Xaml**: Used to provide type information for XAML.

The other way to get type information is to use the SQL provider. Figure 4-10 shows how to use SQL providers, and Figure 4-11 shows how to handle queries.

![](img/63aaf94e22830ab98ce16c5946be8ef6_198_0.png)

FIGURE 4-10 - Using the New Item dialog box to add a SQL type provider

![](img/63aaf94e22830ab98ce16c5946be8ef6_199_0.png)

FIGURE 4-11 - Using the New Item dialog box to add a SQL type provider

## Query

When a type provider brings back a large amount of data, you need sufficient way to process that data. The query is independent of a specific type provider, which means it can be applied to any type provider. To see the query syntax work, look at Listing 4-13, which is a SQL script for creating database tables.

180 PART II F#'s Unique Features

### LISTING 4-13 SQL script for database tables and inserting data

```sql
CREATE TABLE Student(
  StudentID int not null
  constraint PrimaryKey primary key,
  Name varchar(50) null,
  Age int null
);
CREATE TABLE Course(
  CourseID int not null
  constraint PrimaryKey2 primary key,
  CourseName varchar(max) null
);
CREATE TABLE AnotherStudentTable (
  StudentID int not null
  constraint PrimaryKey3 primary key,
  Name varchar(50) null,
  Age int null
);
go
CREATE TABLE CourseSelection(
  StudentID int not null
  constraint foreignKey references dbo.Student(StudentID),
  CourseID int not null
  constraint PrimaryKey2 references dbo.Course(CourseID),
  ID int null
);
go
INSERT Student VALUES (1, 'Lisa', 21)
INSERT Student VALUES (2, 'Brent', 22)
INSERT Student VALUES (3, 'Anita', 20)
INSERT Student VALUES (4, 'Ken', 22)
INSERT Student VALUES (5, 'Cathy', 22)
INSERT Student VALUES (6, 'Tom', 20)
INSERT Student VALUES (7, 'Zeoy', 21)
INSERT Student VALUES (8, 'Mark', 23)
INSERT Student VALUES (9, 'John', null)
go
INSERT COURSE VALUES (1, 'Math')
INSERT COURSE VALUES (2, 'Physics')
INSERT COURSE VALUES (3, 'Biology')
INSERT COURSE VALUES (4, 'English')
go
INSERT CourseSelection VALUES(1, 1, null)
INSERT CourseSelection VALUES(2, 1, null)
INSERT CourseSelection VALUES(3, 1, null)
INSERT CourseSelection VALUES(2, 3, null)
INSERT CourseSelection VALUES(3, 2, null)
```
