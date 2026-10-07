
# Data Selection Query with Visual C#.NET

# 243

| RTOSelect Project | cmdLogIn_Click(object sender, EventArgs e) |
|---|---|
| | private void cmdLogIn_Click(object sender, EventArgs e) |
| A | string cmdString = "SELECT user_name, pass_word, faculty_id, student_id FROM Login WHERE (user_name=@name) AND (pass_word=@word)"; |
| B | SqlCommand cmd = new SqlCommand(); |
| | SelectionForm form = new SelectionForm(); |
| | SqlDataReader dataReader; |
| C | sqlConnection.Open(); cmd.Connection = sqlConnection; |
| | cmd.CommandType = CommandType.Text; |
| | cmd.CommandText = cmdString; |
| D | cmd.Parameters.Add("@name", SqlDbType.Char).Value = txtUserName.Text; |
| | cmd.Parameters.Add("@word", SqlDbType.Char, 8).Value = txtPassword.Text; |
| E | if (dataReader = cmd.ExecuteReader()) |
| F | { |
| | this.Hide(); |
| | form.ShowDialog(); |
| | sqlConnection.Close(); |
| | this.Close(); |
| } |
| G | } else { |
| H | MessageBox.Show("No matched username/password found!"); |
| | cmd.Dispose(); |
| | dataReader.Close(); |
| } |
| } |

FIGURE 5.72 The code for the LogIn button click method.

- E. The ExecuteReader() method is called to perform the data query and the returned data should be filled in the DataReader.
- F. If the returned DataReader contains queried data, its HasRows property should be true, and then the project should go to the next step and the Selection Form should be displayed. The database connection is closed and the current Form, Login Form, should be removed from the project by executing the Close() method.
- G. Otherwise, an error message is displayed to indicate this situation.
- H. Cleaning job is performed to release all data components used in this method.

The coding process for the Cancel button Click method is simple. The function of this method is to cancel the login process due to some reasons and exit the project. This method and enter the codes in Figure 5.73 into this method.

| RTOSelect Project | cmdCancel_Click(object sender, EventArgs e) |
|---|---|
| | private void cmdCancel_Click(object sender, EventArgs e) |
| | { if (sqlConnection.State == ConnectionState.Open) |
| | { |
| | sqlConnection.Close(); |
| | sqlConnection.Dispose(); |
| | } |
| | Application.Exit(); |
| }} |

FIGURE 5.73 The codes for the cancel button click method.

# SQL Server Database Programming with C#

# RTOSlect Project

```csharp
namespace RTSelect_Project
{
    public partial class SelectionForm : Form
    {
        Faculty facultyForm = new FacultyForm();
        CourseForm courseForm = new CourseForm();
        StudentForm studentForm = new StudentForm();

        public SelectionForm()
        {
            InitializeComponent();
            this.ComboSelection.Items.Add("Faculty Information");
            this.ComboSelection.Items.Add("Course Information");
            this.ComboSelection.Items.Add("Student Information");
            this.ComboSelection.SelectedIndex = 0;
        }

        private void cmdOK_Click(object sender, EventArgs e)
        {
            if (this.ComboSelection.Text == "Faculty Information")
            {
                facultyForm.Show();
            }
            else if (this.ComboSelection.Text == "Course Information")
            {
                courseForm.Show();
            }
            else
            {
                studentForm.Show();
            }
        }

        private void cmdExit_Click(object sender, EventArgs e)
        {
            courseForm.Close();
            facultyForm.Close();
            studentForm.Close();
            Application.Exit();
        }
    }
}
```

FIGURE 5.74 The complete codes for the Selection Form window.

# 5.15.4 THE CODING PROCESS FOR THE SELECTION

The function of this Form is to enable users to select different items to perform related query via different window Forms. When an item is selected and the OK button is clicked by the user, the selected window Form is opened to users to perform a related data query to the desired table in our sample database. Double-click on the OK button from the Selection Form window to open its Click, and enter the codes in Figure 5.74 into method. Let's have a closer look at this code of how to use it.

- A. Three new Form objects, facultyForm, StudentForm and courseForm, are created on three classes, FacultyForm, StudentForm and CourseForm, since we need to show one of them is selected by the users to enable perform related query to the related data table in our sample database.
- B. Three selection items are added to the SelectionComboBox to enable users to select one of the project results.
- C. The SelectedIndex = 0 indicates that the first item is selected as a default item.
- D. If the OK button is clicked by the user, a sequence of if-else statements is used to identify which item has been selected. If the Faculty Information is chosen, the facultyForm is displayed.
- E. If the Course Information is chosen, the courseForm is displayed.
- F. Otherwise, the Student Information is selected and displayed.

# Data Selection Query with Visual#.NET

- G. If the Exit button is clicked by the users, all Form objects are closed and we exit the project.

# 5.15.5 QUERY DATA USING THE GENERAL RUNTIME OBJECTS FOR THE FACULTY FORM

- A. Two namespaces, System.IO and System.Data.SqlClient, are added into this code since we need to use some components and methods.
- B. A new object, loginForm, which based on the LoginForm class is generated. The main reason we need this object is to set and use an active connection to our sample database. Recall that in Figure 5.69, a database object sqlConnection was created in the constructor.
- C. Inside the Faculty Form constructor, all first faculty names are added into the Faculty Name combobox. This property enables users to select one of them to perform data query for the selected member as the project runs.
- D. The first method is selected as a default one = 0.
- E. Two different methods, DataAdapter Method and DataReader Method, are also added into the Query method to enable users to select one of them to perform related data query as the project runs.
- F. Similarly, the first method is selected as a default query by setting the SelectedIndex property to 0.
- G. After a new object loginForm is generated in step B, we need to check whether a database connection object sqlConnection should be created that new object is generated, is available. If sqlConnection returns a null, which means that the database connection failed, a warning message is displayed to indicate that situation and the project should be executed if that situation really happened.
- H. The details of the Back Click method start from here.
- I. Before we close this Faculty Form and return to the Selection Form, we need to check whether a database connection is still active. If it is, we need to set that connection and dispose it.
- J. We closed the loginForm window by executing the Close() method since we no longer need it.
- K. The current Form window is temporarily closed by executing the Hide() method since we can permanently close this Form as the Exit button on the Selection Form is clicked.

Our next coding is for the Select Click method. When this is clicked, the faculty name selected by the user from the ComboBox box will be the query criterion to retrieve back all information for selected faculty and displayed in TextBoxes and a PictureBox control PhotoBox in the Faculty Form window.
