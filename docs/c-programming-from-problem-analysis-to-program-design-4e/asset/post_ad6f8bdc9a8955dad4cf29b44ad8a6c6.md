
### TABLE 14-6 OleDbDataReader class members

| OleDbDataReader members | Description |
|---|---|
| `Close()` | Closes an `OleDbDataReader` object |
| `FieldCount` | Property; gets the number of columns in the current row |
| `GetBoolean(int)` | Gets the value of the specified column as a Boolean |
| `GetChar(int)` | Gets the value of the specified column as a `char` |
| `GetDecimal(int)` | Gets the value of the specified column as a `decimal` |
| `GetDouble(int)` | Gets the value of the specified column as a `double` |
| `GetInt16(int)`, `GetInt32(int)`, `GetInt64(int)` | Gets the value of the specified column as an integer |
| `GetName(int)` | Gets the name of the specified column as a `string` |
| `GetOrdinal(string)` | Given the name of the column, gets the ordinal location |
| `GetString(int)` | Gets the value of the specified column as a `string` |
| `GetType(int)` | Gets the type of a specified column |
| `Read()` | Advances the `OleDbDataReader` object to the next record |

**NOTE** A number of the methods in Table 14-6 begin with `Get`, followed by a data type, such as `GetString()`. These methods are called **typed accessors**.

Example 14-10 illustrates using the data reader to process results retrieved using the SQL command. In this example, the values are first stored in an `object`, a member of the `Member` class. The `Member` object is then used to populate a list box object for a Windows application.

### EXAMPLE 14.10

```csharp
Member aMember;
OleDbDataReader dbReader;
dbReader = dbCmd.ExecuteReader(); // dbCmd is the OleDbCommand object
// instantiated in Example 14-3.
while (dbReader.Read())
{
    // Retrieve records 1-by-1...
    aMember = new Member(dbReader["FirstName"].ToString(),
        dbReader["LastName"].ToString());
    this.lstBxMembers.Items.Add(aMember);
}
```

Example 14-11 shows the statements that make up the Member class. Notice that one of the constructors of the Member class accepts two string arguments. In Example 14-10, a Member object, aMember, is instantiated using two of the retrieved dbReader objects. The database field names (from Figure 14-1) are used as indexers with the retrieved dbReader object. Notice how the ToString() method is called with the dbReader object in Example 14-10. This is because the dbReader returns each data field as an object. You have to do the type conversion before sending it to the Member constructor; otherwise, an exception is thrown. For the sake of brevity, the Member class shown in Example 14-11 contains only the read-only properties, a ToString() method, and two constructors.

### EXAMPLE 14.11

```csharp
// Member.cs
// This class includes private members of
// identification number, first and last
// names, and local phone number. Read-only
// properties are included. The ToString()
// method is overridden to return a formatted
// full name.
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DBExample
{
    public class Member
    {
        private string id;
        private string firstName;
        private string lastName;
        private string phoneNumber;

        public Member()
        {
        }

        // Constructor
        public Member(string fname, string lname)
        {
            firstName = fname;
            lastName = lname;
        }

        public string FirstName
        {
            get
            {
                return firstName;
            }
        }

        public string LastName
        {
            get
            {
                return lastName;
            }
        }

        public string Id
        {
            get
            {
                return id;
            }
        }

        public string PhoneNumber
        {
            get
            {
                return phoneNumber;
            }
        }

        public override string ToString()
        {
            return firstName + " " + lastName;
        }
    }
}
```

One last thing should be added to your program statements for the class that is accessing the database. You should always close the connections before exiting the application.

## CLOSING THE CONNECTION

This is one of the easiest things to do, but is often overlooked. You need to close the reader object and the connection object. By doing this, you unlock the database so that other applications can access it. Example 14-12 includes calls to the `Close()` method to close the connection and data reader objects instantiated in the previous examples.

### EXAMPLE 14.12

```csharp
dbReader.Close();
dbConn.Close();
```

An exception can be thrown when you attempt to close connections as well as when you are trying to access data. You can also enclose the close connection statements in a try...catch block, alerting the user if problems arise so that corrective action can be taken.

> **NOTE**
> A special using statement can be added to surround the entire block of code accessing a database. When this is added, it is no longer necessary to call the `Close()` methods. All objects are disposed of when the statements included in the using block (surrounded by curly braces) go out of scope.

Example 14-13 pulls together the statements from Examples 14-1, 14-3, 14-11, and 14-12 enclosing them in a try...catch block. For the sake of brevity, some of the Windows Forms Designer generated code is not included in the listing. The application includes a Listbox object for data display and a Label object for displaying error messages. The label is originally set to a null value.

### EXAMPLE 14.13

```csharp
// DBExample.cs
// A Windows application is used as the
// front end to display records retrieved
// from an Access database.
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Data.OleDb;

namespace DBExample
{
    public partial class DbGUI : Form
    {
        private OleDbConnection dbConn;    // Connection object
        private OleDbCommand dbCmd;        // Command object
        private OleDbDataReader dbReader;  // Data Reader object
        private Member aMember;
        private string sConnection;
        private string sql;

        public DbGUI()
        {
            InitializeComponent();
        }

        private void btnLoad_Click(object sender, EventArgs e)
        {
            try
            {
                // Construct an object of the OleDbConnection
                // class to store the connection string
                // representing the type of data provider
                // (database) and the source (actual db).
                sConnection =
                    "Provider=Microsoft.ACE.OLEDB.12.0;" +
                    "Data Source=member.accdb";
                dbConn = new OleDbConnection(sConnection);
                dbConn.Open();

                // Construct an object of the OleDbCommand
                // class to hold the SQL query. Tie the
                // OleDbCommand object to the OleDbConnection
                // object.
                sql = "SELECT * FROM memberTable ORDER " +
                    "BY LastName ASC, FirstName ASC;";
                dbCmd = new OleDbCommand();
                dbCmd.CommandText = sql;
                dbCmd.Connection = dbConn;

                // Create a dbReader object.
                dbReader = dbCmd.ExecuteReader();

                while (dbReader.Read())
                {
                    aMember = new Member
                        (dbReader["FirstName"].ToString(),
                        dbReader["LastName"].ToString());
                    this.lstBxMembers.Items.Add(aMember);
                }
                dbReader.Close();
                dbConn.Close();
            }
            catch (System.Exception exc)
            {
                this.lblMessage.Text = exc.Message;
            }
        }
    }
}
```

> NOTE — Special note: If you do not override the `ToString()` method in the Member class, when you add an object of that class to the list box, you will get a list box full of the member type names.

The output generated from the program listing in Example 14-13, which uses the Member class (illustrated in Example 14-11), is shown in Figure 14-2. Remember that the database was previously displayed in Figure 14-1.

![](img/36e48639a06772bcb0fa1ea2525b33a3_951_0.png)

**FIGURE 14-2** Accessing the member.accdb database using the database reader object

The data reader class enables read-only access to the database. There are situations that require you to change or update the data in the database. This can be
