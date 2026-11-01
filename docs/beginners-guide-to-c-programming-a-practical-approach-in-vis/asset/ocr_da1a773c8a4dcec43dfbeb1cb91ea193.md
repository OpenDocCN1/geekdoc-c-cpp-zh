```
private void updateButton_Click(object sender, EventArgs e)
{
    string path = Environment.CurrentDirectory;
    string databasePath = path + "\\firstDatabase.accdb";
    OleDbConnection myConn = new OleDbConnection("Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" + databasePath);
    myConn.Open();

    string selectedEntry = displayListBox.SelectedItem.ToString();
    int selectedEntry_id_number = int.Parse(selectedEntry.Split('-')[0]);

    MessageBox.Show("The entry with id_number: " + selectedEntry_id_number + " will now be updated.");

    OleDbCommand cmd = new OleDbCommand("UPDATE Table1 SET name_field =?, surname_field =?, age_field=? WHERE id_number = ?", myConn);
    cmd.Parameters.AddWithValue("?", updateNameTextBox.Text);
    cmd.Parameters.AddWithValue("?", updateSurnameTextBox.Text);
    cmd.Parameters.AddWithValue("?", updateAgeTextBox.Text);
    cmd.Parameters.AddWithValue("?", selectedEntry_id_number);

    int cmdResult = cmd.ExecuteNonQuery();
    MessageBox.Show("Number of updated entries: " + cmdResult.ToString());
    myConn.Close();
}
```

Code 15.33

The complete Form1.cs is also given below for your convenience:

```
using System;
using System.Windows.Forms;
using System.Data;
using System.Data.OleDb;

namespace AccessDatabaseManipulation
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }
```