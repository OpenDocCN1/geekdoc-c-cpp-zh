3. Set the Names and Texts of the Buttons as **connectDisconnectButton**, **viewEntriesButton**, **Connect-disconnect** and **View Entries**, respectively.

4. Set the Name of the ListBox as **displayListBox**. The form layout will look as follows:

![](bbox=[0.32, 0.29, 0.68, 0.55])

Figure 15.14. Layout of the form

5. Double-click the Connect-disconnect Button to create its Click event handler connectDisconnectButton_Click(...). We will open and close database connection in this method for test purposes. Firstly, add the following namespace inclusion code lines at the top section of Form1.cs:

```
using System.Data;
using System.Data.OleDb;
```

Code 15.1

We will create an OleDBConnection object inside the connectDisconnectButton_Click(...) method. An OldeDBConnection object is created with the following constructor template:

```
OleDbConnection myConn = new OleDbConnection(@connection string; Data Source= full path of the database file);
```

Code 15.2