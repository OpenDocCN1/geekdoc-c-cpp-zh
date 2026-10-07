D. As the project runs, each time the user clicks the Select button to perform a data query, a request is sent to the database server and the Web server (it can be the same server as the database server). Then the Web server will post a refreshed Faculty page to the client when it received this request (IsPostBack = true). Each time this happened, the Page_Load() method will be activated and duplicated to the end of the combobox ComboName. To avoid this duplication, you need to check the IsPostBack property of the page and add faculty members into the combobox only once when the project starts (IsPostBack = false). Refer to Section 8.4.9 for more detailed discussion about the AutoPostBack property.

Next we need to develop the codes for the Select button's Click method to perform the data query against the database.

# 8.4.8.2 Develop the Codes for the Select Button Method

The function of this piece of codes is to make a query to the database to retrieve the faculty information based on the selected faculty member by user from the Faculty Name combobox control, and display those pieces of retrieved information in text boxes and faculty image on the Faculty page.

Open this Select button's Click method by double-clicking this button on the Design View of the Faculty form, and enter the codes that are shown in Figure 8.23 into this method.
Let's take a closer look at this piece of codes to see how this works.

+   A. The query string that contains a SELECT statement is declared here we need to use this string as our command text. The dynamic parameter of this query is the @name, which is the selected faculty member by the user as the project runs.

+   B. All data components as Command and DataReader objects are declared here we need to use them to perform the data query later.

+   C. The Command object is initialized by assigning the associated components to it. These components include the global connection object that is stored in the Application state, the CommandType and the CommandText.

| SQLWebServerProject | cmdSelect_Click(object sender, EventArgs e) |
|---|---|
| A | protected void cmdSelect_Click(object sender, EventArgs e) { |
| B | string cmd = "SELECT faculty_id, faculty_name, title, phone, college, email, image FROM Faculty "; |
| C | string cmdString = cmd + " FACULTY_name = @name"; |
| D | SqlCommand sqlCommand = new SqlCommand(); |
| E | SqlDataReader sqlDataReader; |
| F | sqlCommand.Connection = new SqlConnection("ConnectionString"); |
| G | sqlCommand.CommandType = CommandType.Text; |
| H | sqlCommand.Parameters.Add("@name", SqlDbType.VarChar,Value = ComboName.Text); |
| I | sqlDataReader = sqlCommand.ExecuteReader(); |
| J | if (sqlDataReader.HasRows) { |
| K | FacultyPage(sqlDataReader); |
| L | } else { |
| M | Response.Write("<script>alert('No matched faculty found!')</script>"); |
| N | sqlDataReader.Close(); |
| O | sqlCommand.Dispose(); |
| P | } |

FIGURE 8.23 The codes for the select button's click method.