10. Let’s build and run the project to see if our List entries Button is working properly. The entries should be listed with the id_number in the ListBox when List entries Button is clicked:

![](bbox=[0.2, 0.25, 0.8, 0.55])

Figure 15.22. Data entries listed in the ListBox

If you cannot see the data or if the program issues an error, please double-check the previous steps before continuing.

11. Let’s now develop the code for the Delete Button. The user will select a line in the ListBox and then he/she will click this Button to delete the selected entry from the database. Firstly, double-click the Delete Button to create its event handler method deleteButton_Click(...).

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