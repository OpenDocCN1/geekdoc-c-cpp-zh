
Please click the Save button. We have now created our sample database and added some data into it in Access itself. It is now time to connect to this database from our own C# program.

## 15.2. Reading Database Entries from our C# Program

Our programs can connect to Access databases via Access Database Engine. If you have an Office suite newer than 2007, Access Database Engine is already installed on your computer. If not, you can download this tool from https://www.microsoft.com/en-us/download/details.aspx?id=13255 (or just Google for "Access Database Engine") and install on your PC.

Databases are accessed using database commands from C# .NET programs. Firstly, a connection to the database is opened. Then, a read or write operation is performed on the database table using database commands. After finishing our job with the database, the connection is closed.

We can use the following objects for accessing and manipulating Access databases:

- **OleDbConnection**: Used for opening or closing a connection to the database. Its constructor method accepts the path to the file and the connection string regarding to the database type.
- **OleDbCommand**: Used for sending queries to the database for selecting and manipulating data.
- **DataReader**: Used for reading data from the database. It is used in conjunction with the OleDbCommand object.
- **OleDbDataAdapter**: Transfers data to a DataSet object.
- **DataSet**: Temporarily stores the data for displaying and manipulating purposes.

Let’s see how we can connect to our firstDatabase.accdb using these objects in a typical example.

1. Create a new C# project.
2. Add two Buttons and a ListBox on the form.
3. Set the Names and Texts of the Buttons as **connectDisconnectButton**, **viewEntriesButton**, **Connect-disconnect** and **View Entries**, respectively.
4. Set the Name of the ListBox as **displayListBox**. The form layout will look as follows:

![](img/41d82527c4e41cdb7e56259564306ddc_359_0.png)

Figure 15.14. Layout of the form

5. Double-click the Connect-disconnect Button to create its Click event handler connectDisconnectButton_Click(...). We will open and close database connection in this method for test purposes. Firstly, add the following namespace inclusion code lines at the top section of Form1.cs:

```csharp
using System.Data;
using System.Data.OleDb;
```

Code 15.1

We will create an OleDbConnection object inside the connectDisconnectButton_Click(...) method. An OleDbConnection object is created with the following constructor template:

```csharp
OleDbConnection myConn = new OleDbConnection(@connection string; Data Source= full path of the database file);
```

Code 15.2

Temporarily stored in an OleDbDataReader object that will be created via this readCommand object:

```csharp
OleDbDataReader reader = readCommand.ExecuteReader();
```

Code 15.9

We will display the read data on the ListBox. Let’s clear the ListBox first:

```csharp
displayListBox.Items.Clear();
```

Code 15.10

And then use a while loop to insert the read data to the ListBox:

```csharp
while (reader.Read())
{
    displayListBox.Items.Add(reader["name_field"].ToString() + " - " + reader["surname_field"] + " - " + reader["age_field"]);
}
```

Code 15.11

The while loop will continue running as long as there is data in the reader object therefore all data of Table1 will be displayed in the ListBox. Finally, don’t forget closing the connection:

```csharp
myConn.Close();
```

Code 15.12

The complete viewEntriesButton_Click() method is also given below:

```csharp
private void viewEntriesButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();
    OleDbCommand readCommand = new OleDbCommand("SELECT name_field, surname_field, age_field FROM Table1", myConn);
    OleDbDataReader reader = readCommand.ExecuteReader();
    displayListBox.Items.Clear();
    while (reader.Read())
    {
        displayListBox.Items.Add(reader["name_field"].ToString() + " - " + reader["surname_field"] + " - " + reader["age_field"]);
    }
    myConn.Close();
}
```

Code 15.13 (cont’d)

7. Build and run the project. The following program window will appear:

![](img/41d82527c4e41cdb7e56259564306ddc_363_0.png)

Figure 15.15. The program window

Firstly, click the Connect-disconnect Button. The program will display the message boxes regarding these operations. If your program gives an error, please double-check the connection string and make sure that the database file is in the same folder as the executable file.

![](img/41d82527c4e41cdb7e56259564306ddc_363_1.png)

Figure 15.16. Database connection opening message

![](img/41d82527c4e41cdb7e56259564306ddc_364_0.png)

Figure 15.17. Database connection closing message

These messages show that our connection object is being created properly, i.e. the connection string is correct and our database file is at the right place. Now, let’s click the View entries Button to read data from the database. The ListBox will be populated by the data we entered in our firstDatabase.accdb file:

![](img/41d82527c4e41cdb7e56259564306ddc_364_1.png)

Figure 15.18. Data read from database shown in the ListBox

We can update/add/remove entries of our database in Access and then click View entries Button again to display the updated data. I have entered new data to Table1 and displayed the updated data in the ListBox as in Figure 15.19.

![](img/41d82527c4e41cdb7e56259564306ddc_365_0.png)

Figure 15.19. The updated data shown in the ListBox

## 15.3. Adding/Updating/Deleting Database Entries from our C# Program

We have manipulated data of the database in Access and displayed the updated data in our program. The problem is that the user may not have Access installed on his/her computer or we may need to manipulate entries of our database in a systematic way in our program. Adding new data, removing entries or updating data are all possible in our own program using the corresponding commands for the OleDbCommand object. Let’s start developing our example project for learning how we can manipulate database entries.

1. Create a new C# project.
2. Add six TextBoxes, six Labels, four Buttons and a ListBox on the form in the following layout shown in Figure 15.20.
3. Set the Names of the TextBoxes from top to down as insertNameTextBox, insertSurnameTextBox, insertAgeTextBox, updateNameTextBox, updateSurnameTextBox and updateAgeTextBox, respectively (confusing, I know!).
4. Set the Names of the Buttons as insertButton, updateButton, listButton and deleteButton in order.
5. Set the Texts of the Buttons as Insert, Update, List entries and Delete selected, respectively.
6. Set the Texts of the Labels as Name:, Surname:, Age:, Name:, Surname: and Age:, respectively.
7. Finally, set the Name of the ListBox as displayListBox. The form will look as in Figure 15.21 after these modifications.

![](img/41d82527c4e41cdb7e56259564306ddc_366_0.png)

Figure 15.20. Layout of the form

![](img/41d82527c4e41cdb7e56259564306ddc_366_1.png)

Figure 15.21. The form after setting the Text properties

8. Copy our sample Access database file, firstDatabase.accdb to /bin/debug folder under the project folder.
9. Let's implement the event handler method of the List entries Button borrowing code from the previous example since we have already developed the code for displaying data in the ListBox. Double-click the List entries Button to create its event handler method. Copy and paste Code 15.13 to listButton_Click() for displaying the database entries in the ListBox. But we will have a small modification here. This time we will display the id_number too in addition to name,
