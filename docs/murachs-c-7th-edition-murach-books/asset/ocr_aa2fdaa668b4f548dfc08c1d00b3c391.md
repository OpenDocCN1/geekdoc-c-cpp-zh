# Parameters for the Scaffold-DbContext command

| Parameter | Description |
|---|---|
| -Connection | The connection string for the database. This parameter is required. |
| -Provider | The provider, often a NuGet package name. This parameter is required. |
| -OutputDir | The folder where the generated files are stored. The default is the root folder for the project. |
| -Context | The name for the generated DB context file. |
| -DataAnnotations | Specifies that attributes are used to configure the entity classes whenever possible. Otherwise, EF uses the Fluent API to perform all configuration. |
| -UseDatabaseNames | Specifies that entity classes and properties are given the same names as the tables and columns in the database. Otherwise, EF uses names that conform to C# conventions. |
| -Force | Specifies that existing files can be overwritten. Otherwise, existing files can’t be overwritten. |

# Common values used in a connection string for SQL Server Express LocalDB

| Name | Description |
|---|---|
| Data Source/Server | The name of the instance of SQL Server you want to connect to. |
| AttachDbFilename | The path and file name for the database’s .mdf file. |
| Integrated Security | Determines whether the connection is secure. Valid values are True, False, and SSPI. SSPI uses Windows integrated security and is equivalent to True. |

# A Scaffold-DbContext command for a Sql Server Express LocalDB database

```
PM> Scaffold-DbContext -Connection "Data Source=(LocalDB)\MSSQLLocalDB; AttachDBFilename=C:\#\Database\MMABooks.mdf;Integrated security=True" -Provider Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models\DataLayer -Context MMABooksContext -DataAnnotations -Force
```

# The same command with the flags for the required parameters omitted

```
PM> Scaffold-DbContext "Data Source=(LocalDB)\MSSQLLocalDB; AttachDBFilename=C:\#\Database\MMABooks.mdf;Integrated security=True" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models\DataLayer -Context MMABooksContext -DataAnnotations -Force
```

# Description

+   - With *Database First development*, you generate database (DB) context and entity classes from an existing database. To do that, you can use the Scaffold-DbContext command.
+   - The *DB context class* is used to communicate with the database, and the *entity classes* represent the objects used by the application.
+   - You enter the Scaffold-DbContext command in the NuGet Package Manager Console (PMC) window. To display this window from Visual Studio, select Tools→NuGet Package Manager→Package Manager Console.
+   - When you use the Scaffold-DbContext command, you can omit the parameter flags for required parameters. If you do that, you need to code the value for the -Connection parameter first, followed by the value for the -Provider parameter.