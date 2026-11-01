```
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
        displayListBox.Items.Add(reader["id_number"] + "-" +
            reader["name_field"].ToString() + " " +
            reader["surname_field"] + " - " +
            reader["age_field"]);
    }
    myConn.Close();
}

private void deleteButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();
    string selectedEntry = displayListBox.SelectedItem.ToString();
    int selectedEntry_id_number = int.Parse(selectedEntry.Split('-')[0]);
    MessageBox.Show("The entry with id_number: " + selectedEntry_id_number + " will now be deleted.");
    OleDbCommand cmd = new OleDbCommand("DELETE FROM Table1 WHERE id_number=?", myConn);
    cmd.Parameters.AddWithValue("?", selectedEntry_id_number);
    int cmdResult = cmd.ExecuteNonQuery();
    MessageBox.Show("Number of deleted entries: " + cmdResult.ToString());
}
```