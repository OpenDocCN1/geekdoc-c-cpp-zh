open, but opening a Connection on the current database’s Connection property provides all those settings. CurrentProject.Connection is actually a long string (specifically, a connection string) that includes all the information needed about the current database. A typical Connection property setting is as follows:

```
Provider=Microsoft.ACE.OLEDB.12.0;User ID=Admin;
Data Source=C:\...\Chapter28.accdb;
Mode=Share Deny None;Extended Properties="";
Jet OLEDB:System database=C:\...\Microsoft\Access\System.mdw;
Jet OLEDB:Registry Path=Software\...\Access Connectivity Engine;
Jet OLEDB:Database Password="";
Jet OLEDB:Engine Type=6;
Jet OLEDB:Database Locking Mode=1;
Jet OLEDB:Global Partial Bulk Ops=2;
Jet OLEDB:Global Bulk Transactions=1;
Jet OLEDB:New Database Password="";
Jet OLEDB:Create System Database=False;
Jet OLEDB:Encrypt Database=False;
Jet OLEDB:Don’t Copy Locale on Compact=False;
Jet OLEDB:Compact Without Replica Repair=False;
Jet OLEDB:SFP=False;
Jet OLEDB:Support Complex Data=True;
Jet OLEDB:Bypass UserInfo Validation=False;
Jet OLEDB:Limited DB Caching=False;
Jet OLEDB:Bypass ChoiceField Validation=False
```

# NOTE

Line breaks have been added to the preceding code for clarity, and some lines have been shortened.

This is actually considerably more than the Connection object actually needs, but Microsoft wanted to make sure nothing was missing.

Notice the Data Source portion of the ConnectionString property. This is the part that points to a specific ACCDB file. Changing this path means the Connection object can open virtually any Access database as long as the path is valid and points to an ACCDB file.

The following procedure opens a Connection against the current database, prints the Connection object’s Provider property, and then closes and discards the Connection object:

```
Public Sub OpenConnection()

    Dim adConn As ADODB.Connection

    Set adConn = New ADODB.Connection
    adConn.Open CurrentProject.Connection
```