```
```csharp
myConn.Close();
}
private void insertButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;DataSource=" + databasePath);
    myConn.Open();
    OleDbCommand cmd = new OleDbCommand("INSERT INTO Table1(name_field,surname_field,age_field) VALUES (?,?,?)", myConn);
    cmd.Parameters.AddWithValue("?", insertNameTextBox.Text);
    cmd.Parameters.AddWithValue("?", insertSurnameTextBox.Text);
    cmd.Parameters.AddWithValue("?", insertAgeTextBox.Text);
    int cmdResult = cmd.ExecuteNonQuery();
    MessageBox.Show("Number of inserted entries: " + cmdResult.ToString());
    myConn.Close();
}
private void updateButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection(@"Provider=Microsoft.ACE.OLEDB.12.0;DataSource=" + databasePath);
    myConn.Open();
    string selectedEntry = displayListBox.SelectedItem.ToString();
    int selectedEntry_id_number = int.Parse(selectedEntry.Split('-')[0]);
    MessageBox.Show("The entry with id_number: " + selectedEntry_id_number + " will now be updated.");
    OleDbCommand cmd = new OleDbCommand("UPDATE Table1 SET name_field =?, surname_field =?, age_field=? WHERE id_number =?", myConn);
    cmd.Parameters.AddWithValue("?", updateNameTextBox.Text);
```
```