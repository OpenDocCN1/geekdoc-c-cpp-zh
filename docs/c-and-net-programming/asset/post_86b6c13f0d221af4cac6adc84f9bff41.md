
| No. | Feature | Description |
|---|---|---|
| 6. | Web services | .NET Compact Framework applications can consume Web services, but they can't provide them due to the lack of a hosting Web server. |
| 7. | XML support | .NET Compact Framework applications will have full support for reading and writing XML using the reader and writer classes, but they won't have support for XSLT or XPath. |
| 8. | COM Interop | Unsupported in .NET Compact Framework. |
| 9. | OLE DB Wrapper | Not supported in .NET Compact Framework. |
| 10. | .NET Remoting | Unsupported in .NET Compact Framework, but XML services are to be used as an alternative for this. |
| 11. | Win32 Calls | .NET Compact Framework does not support calls from Win32; one can make calls from Compact Framework into Win32. Communication between Win32 and Compact Framework is done by the MessageWindow class. But one-way communication is supported in the Compact Framework. |
| 12. | DataGrids | Not built in to the editing support as in the .NET Framework. The .NET Compact Framework can only bind DataGrids to a single table object. The .NET Compact Framework only displays rows from a single table, and these are not able to be expanded as in the .NET Framework. |
| 13. | Tooltips | This GUI control is unsupported in the .NET Compact Framework but supported in the .NET Framework. |
| 14. | Windows Forms controls | No drag-and-drop support, no printing, no checked list box, no ActiveX support, and no GDI+ in the .NET Compact Framework. Out of a total of 35 controls, the .NET Compact Framework supports approximately only 28 controls. |
| 15. | File change notifications | This is supported on the .NET Framework but not supported on the .NET Compact Framework due to OS constraints. |
| 16. | nGen (Install-time JIT) | Unsupported in .NET Compact Framework. |

## 28.2 Compact Edition Data Stores - SQL Server CE

- The most preferable repository to store data in a Pocket PC is a SQL database. But the most important point is that one cannot install the desktop SQL Server in a Pocket PC due to memory constraints; for this, Microsoft came up with SQL Server CE (Compact Edition), which is now called Mobile SQL.
- Microsoft SQL Server CE is a very compact relational database that runs on smart devices and has built-in support for the .NET Compact Framework. It can support databases up to 2 GB in size and also supports binary large objects (BLOBs) up to 1 GB. It should be noted that the size of the local database is limited by the storage size available on the smart device.
- SQL Server CE is an ideal storage mechanism due to its capabilities for encryption for security purposes. This is also great for data connections that are wireless connections and/or online/offline connections. The most interesting point is that the SQL CE data provider provides almost a similar kind of flavor to that available for the SQL Server 2000 data provider.
- The major components of SQL CE are the database engine, client agent, and Query Analyzer (isql.exe). The Query Analyzer program allows a graphical interface to create and structure a database in a tree view form (this allows a graphical representation of the database objects). The Query Analyzer can be used to perform updates to data, a selection of data, or insert/delete data in the local database and on top of it expose the data as an XML document for use with Web-based applications.
- SQL CE supports data types like integer, numeric, binary, nchar/nvarchar, etc.
- .NET Compact Framework provides ADO.NET to interact with the CE edition of the database (it is SQL Server CE 2.0 in the current topic).
- ADO.NET for SQL CE data providers are System.Data and System.Data.SqlServerCe.

### Process to develop an application to use SQL Server CE

**Step 1:** Check whether the database is available or not; if not, create the database through the SqlCeEngine object as below.

```csharp
if (!File.Exists(@"\My Documents\TechAuthorsDB.sdf"))
{
    SqlCeEngine empEngine = new SqlCeEngine("Data Source = \\My Documents\\TechAuthorsDB.sdf");
    empEngine.CreateDatabase();
}
```

Note: The database file name must have .sdf extension.

**Step 2:** After the database is created, the next step is to create the required tables.

```csharp
SqlCeConnection techCon;
SqlCeCommand techCom;
techCon = new SqlCeConnection("Data Source = \\My Documents\\TechAuthorsDB.sdf");
techCon.Open();
techCom = techCon.CreateCommand();
string strQuery = "CREATE TABLE Authors (AID int IDENTITY(0,1) PRIMARY KEY, AName nvarchar(10), Titles int)";
techCom.CommandText = strQuery;
techCom.ExecuteNonQuery();
```

This code snippet creates a table with three columns (AID, AName, and Titles).

**Step 3:** Once the database is set up, then further operations to store or fetch data can be done through SqlCeDataReader as shown below.

```csharp
string strQuery = "SELECT * FROM Authors ORDER BY AName ASC";
techCom.CommandText = strQuery;
SqlCeDataReader techReader = techCom.ExecuteReader();
```

## 28.3 .NET Compact Framework - Errors, Testing and Debugging

### 28.3.1 .NET Compact Framework - Errors and Exceptions

- Error handling and tracing have always been a challenge, and many attempts have been made to automate error handling. .NET Compact Framework has supported error handling by including e-mailing of logs. Due to the limitations of the Compact Framework, one does not get as much support as in the full framework, but it works really well.

Below are a few errors that can occur in mobile device applications:

- 1. The operation has been cancelled — There are two known possible reasons for this error:
  - i. Some devices display a confirmation dialog box. If one doesn't explicitly agree, then it generates an error.
  - ii. There's a 1-minute timeout for copying the profiler core .dll file and profiler core .pdb file to the Windows folder in the device. This error might be raised if data transfer speed is low.
- 2. **Invalid Index error in tracing mode** — Most likely this error is caused by a known bug in .NET Compact Framework 3.5. The best workaround is switching to **Sampling** profiling.
- 3. **Can't connect to host, unsupported instruction set** — Most likely this error is generated when one is trying to profile a Windows CE 4.x application, which is not supported by certain performance enhancement applications.

### Exception Handling

- During the execution of an application, unforeseen events sometimes transpire. To handle these gracefully, the Compact Framework supports structured exception handling (SEH), as does the desktop Framework. This allows developers to use try-catch semantics in their code and to test for specific types of exceptions thrown by the application. The Execution Engine (EE) of the Compact Framework is optimized for the non-exceptional case, and so throwing exceptions should be reserved for true exceptions and not simply to signal a normal occurrence. **The key difference in exception handling in the Compact Framework is that the error strings are actually stored in a separate assembly, System.SR.dll**. This is due to the resource constraints of devices and allows the developer optionally to install this assembly on the device. If required, the EE will load it and display the appropriate message, and, if not, a default message will be displayed.
- Exceptions thrown by .NET Compact Framework are different from those thrown by .NET Framework. **EntryPointNotFoundException** and **ExecutionEngineException** are thrown by .NET Framework if the function cannot be located or the function is declared improperly, whereas in the case of .NET Compact Framework **NotSupportedException** and **MissingMethodException** are thrown.
- **NotSupportedException**: Many of the features supported by P/Invoke in the .NET Framework are not supported in the .NET Compact Framework. **NotSupportedException** is thrown when the declaration is incorrect or the restrictions imposed by the .NET Compact Framework are violated.
- **MissingMethodException** — This exception is thrown mainly because of the following reasons:
  - 1. Function name is incorrect.
  - 2. Parameters passed to the functions are incorrect.
  - 3. Marshalling issues on non-blittable type.
  - 4. The DLL being called using P/Invoke is not dependent on other DLLs (which might be missing).
