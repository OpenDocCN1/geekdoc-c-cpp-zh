# Data Selection Query with C#.NET

![](bbox=[0.277, 0.085, 0.722, 0.305])

FIGURE 5.70 The Modified LogIn window.

Now open the LogForm window by right-clicking on the Login.cs from the Explorer window and select the View Designer button, and then double-click the TabLogin button to open its Click Method. The codes, which are shown in Figure 5.71, into this method. Let's have a closer look at this piece of codes to see how it works.

A. The query string for the SQL server database is declared. first query contained two dynamic parameters, Username and Password.

| RTOSelect Project | cmdTabLogIn_Click(object sender, EventArgs e) |
|---|---|
| A | private void cmdTabLogIn_Click(object sender, EventArgs e) {
string cmdString += "SELECT user_name, pass_word, faculty_id, student_id FROM Login";
cmdString += "WHERE (user_name=@Param1) AND (pass_word=@Param2)"; |
| B | SqlDataAdapter dataAdapter = new SqlDataAdapter();
DataTable dataTable = new DataTable();
SqlCommand cmdCommand = new SqlCommand();
SelectionForm sel = new SelectionForm(); |
| C | cmdCommand.Connection = SqlConnection;
cmdCommand.CommandType = CommandType.Text;
cmdCommand.CommandText = cmdString; |
| D | cmdCommand.Parameters.Add("@Param1", SqlDbType.Char, 8).Value = txtUserName.Text; |
| E | cmdCommand.Parameters.Add("@Param2", SqlDbType.Char, 8).Value = txtPassWord.Text;
LogDataAdapter.Select = cmdCommand;
LogDataAdapter.Fill(dataTable); |
| F | if (dataTable.Rows.Count > 0) {
this.Hide();
selForm.ShowDialog();
sqlConnection.Close();
this.Close();
} |
| G | else {
MessageBox.Show("No matched username/password found!");
dataTable.Dispose();
} |
| H | sqlCommand.Dispose();
LogDataAdapter.Dispose();
}

FIGURE 5.71 The codes for the TabLogin button click method.