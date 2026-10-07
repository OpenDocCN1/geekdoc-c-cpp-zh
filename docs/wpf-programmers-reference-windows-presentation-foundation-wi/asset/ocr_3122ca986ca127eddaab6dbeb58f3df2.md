> Note that you don't need to have Access installed on your computer to use an Access database in your program. You only need a database engine that can open the database, such as the Jet database engine.

If you modify any of the student values in the middle, the controls automatically update the responding ADO.NET objects. If you use the Data “Save Changes” command, the program writes those changes back into the database.(This example does not provide a way to add or delete students, or to add or modify a student's test.)

The database has a third named States that lists the U.S. states (plus Washington, DC) and their abbreviations. The program uses this as a lookup table. The Students contains each student's state as an abbreviation. When it displays the value, the ComboBox in the middle of the window uses the States table to convert the abbreviation into the state's full.

The following sections explain how the program performs its major tasks.

# Loading Data

The following code shows how the StudentData program loads its data from the database:

```
OleDbDataAdapter m_daUsers;
DataSet m_dsStudentData;
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    // Connect to the database.
    OleDbConnection conn = new OleDbConnection(
        "Provider=Microsoft.OLEDB.4.0;Data Source=StudentData.mdb";
    )
    try {
        // Open the connection.
        conn.Open();

        // The Dataset to hold all of the data.
        m_dsStudentData = new DataSet();

        // Load Students table.
        m_daUsers = new OleDbDataAdapter();
        m_daUsers.SelectCommand = 
            new OleDbCommand("SELECT * FROM Students ORDER BY FirstName, LastName, conn");
        m_daUsers.Fill(m_dsStudentData, "Students");

        // Load TestScores table.
        OleDbDataAdapter dataScores = new OleDbDataAdapter();
        dataScores.SelectCommand = 
            new OleDbCommand("SELECT * FROM TestScores, conn");
        dataScores.Fill(m_dsStudentData, "TestScores");
```