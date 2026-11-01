
surname and age fields because we will need this information for other operations. We just need to create the readCommand as follows to include the id_number too :

```
OleDbCommand readCommand = new OleDbCommand("SELECT
    name_field, surname_field, age_field FROM Table1",
    myConn);
```

Code 15.14

Also, add the database entries in the while loop using the following Add() method to add id_number too:

```
displayListBox.Items.Add(reader["id_number"] + "-" +
    reader["name_field"].ToString() + "-" +
    reader["surname_field"] + "-" +
    reader["age_field"]);
```

Code 15.15

Our listButton_Click() method will be as follows after these small modifications:

```csharp
private void listButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();
    OleDbCommand readCommand = new OleDbCommand("SELECT id_number, name_field, surname_field, age_field FROM Table1", myConn);
    OleDbDataReader reader = readCommand.ExecuteReader();
    displayListBox.Items.Clear();
    while (reader.Read())
    {
        displayListBox.Items.Add(reader["id_number"] + "-" + reader["name_field"].ToString() + "-" + reader["surname_field"] + "-" + reader["age_field"])
    }
    myConn.Close();
}
```

Code 15.16

10. Let's build and run the project to see if our List entries Button is working properly. The entries should be listed with the id_number in the ListBox when List entries Button is clicked:

![](img/41d82527c4e41cdb7e56259564306ddc_368_0.png)

Figure 15.22. Data entries listed in the ListBox

If you cannot see the data or if the program issues an error, please double-check the previous steps before continuing.

11. Let's now develop the code for the Delete Button. The user will select a line in the ListBox and then he/she will click this Button to delete the selected entry from the database. Firstly, double-click the Delete Button to create its event handler method deleteButton_Click(...).

12. Firstly, we will open our connection:

```
string path = Environment.CurrentDirectory;
string databasePath = path + "\\firstDatabase.accdb";
OleDbConnection myConn = new
OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
myConn.Open();
```

Code 15.17

13. Then we will take the selected entry in the ListBox and then get its id_number with the following code lines:

```csharp
string selectedEntry = displayListBox.SelectedItem
    .ToString();
int selectedEntry_id_number = int.Parse(selectedEntry
    .Split('-')[0]);
MessageBox.Show("The entry with id_number: " + 
    selectedEntry_id_number + " will now be deleted.");
```

Code 15.18

In the first line, we get the whole text of the selected line in the ListBox. And then parse this text to get the first part before the hyphen, which is the id_number. We display a message box informing the user about the entry to be deleted.

14. We will then form the required query that will perform the deletion as follows:

```csharp
OleDbCommand cmd = new OleDbCommand("DELETE FROM Table1
    WHERE id_number=?", myConn);
cmd.Parameters.AddWithValue("?", selectedEntry_id_number);
```

Code 15.19

We constructed a new OleDbCommand object with the query line ("DELETE FROM Table1 WHERE id_number=?" which will operate on myConn. We pass the id_number we obtained before. We use the "?" symbol for passing the id_number by adding it as a parameter to the query.

15. Finally, we execute the cmd object as follows:

```csharp
int cmdResult = cmd.ExecuteNonQuery();
MessageBox.Show("Number of deleted entries: " + 
    cmdResult.ToString());
myConn.Close();
```

Code 15.20

The ExecuteNonQuery() is the method that actually runs the query. It returns the number of entries affected by the query. We store this result in a variable named cmdResult. We then display the information regarding the number of affected entries and then close the connection. The whole deleteButton_Click(...) is also shown below for completeness:

```
private void deleteButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new
        OleDbConnection("Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();

    string selectedEntry =
        displayListBox.SelectedItem.ToString();
    int selectedEntry_id_number =
        int.Parse(selectedEntry.Split('-')[0]);

    MessageBox.Show("The entry with id number: " +
        selectedEntry_id_number + " will now be deleted.");

    OleDbCommand cmd = new OleDbCommand("DELETE FROM Table1
        WHERE id_number=?", myConn);
    cmd.Parameters.AddWithValue("?",
        selectedEntry_id_number);

    int cmdResult = cmd.ExecuteNonQuery();
    MessageBox.Show("Number of deleted entries: " +
        cmdResult.ToString());
    myConn.Close();
}
```

Code 15.21

16. Build and run the project to see if everything is OK for now. Firstly click the List entries Button to display the database entries in the ListBox:

![](img/41d82527c4e41cdb7e56259564306ddc_370_0.png)

Figure 15.23. Database entries listed in the ListBox

Click to select an entry in the ListBox. I selected the second one:

![](img/41d82527c4e41cdb7e56259564306ddc_371_0.png)

Figure 15.24. The second entry is selected

Now, click the Delete selected Button. The program will issue a message regarding the id_number of the entry to be deleted as in Figure 15.25. Then the entry will be deleted from the database and then the information showing the affected entries will be displayed as shown in Figure 15.26.

![](img/41d82527c4e41cdb7e56259564306ddc_371_1.png)

Figure 15.25. The message box displaying deletion information

## CHAPTER 15. DATABASE CONNECTIONS USING ADO.NET

![](img/41d82527c4e41cdb7e56259564306ddc_372_0.png)

Figure 15.26. Message box showing the number of deleted entries

Click the List entries Button to see if the selected entry is actually deleted from the database. It is deleted successfully proving that our Delete Button works as expected as shown below:

![](img/41d82527c4e41cdb7e56259564306ddc_372_1.png)

Figure 15.27. The entries of the database displayed after the deletion of the second entry

17. We are now ready to implement the insert operation. We will take the Name, Surname and Age inputs and insert them in a new entry in the database when the Insert Button is clicked. Double-click the Insert Button to create its Click event handler insertButton_Click().

We will write the code of the insertButton_Click() method. Firstly, copy and paste the standard database connection part as we implemented before:

```csharp
string path = Environment.CurrentDirectory;
string databasePath = path + "\\firstDatabase.accdb";
OleDbConnection myConn = new
OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
myConn.Open();
```
Code 15.22

Now, create an OleDbCommand object which will hold the insertion query as follows:

```csharp
OleDbCommand cmd = new OleDbCommand("INSERT INTO Table1(name_field,surname_field,age_field) VALUES (?,?,?)", myConn);
```
Code 15.23

We will pass the name_field, surname_field and age_field strings from the insertNameTextBox, insertSurnameTextBox and insertAgeTextBox with the utilization of "?" parameters:

```csharp
cmd.Parameters.AddWithValue("?", insertNameTextBox.Text);
cmd.Parameters.AddWithValue("?", insertSurnameTextBox.Text);
cmd.Parameters.AddWithValue("?", insertAgeTextBox.Text);
```
Code 15.24

Finally, execute the query command with the ExecuteNonQuery() method as we did in the Delete Button:

```csharp
int cmdResult = cmd.ExecuteNonQuery();
MessageBox.Show("Number of inserted entries: " + cmdResult.ToString());
myConn.Close();
```
Code 15.25
