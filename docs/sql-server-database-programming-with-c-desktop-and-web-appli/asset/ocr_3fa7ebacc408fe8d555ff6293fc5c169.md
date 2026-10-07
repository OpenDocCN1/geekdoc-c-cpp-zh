# Data Inserting with Visual C#.NET

| RTOInsert Project | cmdInsert_Click(object sender, EventArgs egs) |
|---|---|
| private void cmdInsert_Click(object sender, EventArgs egs) { |
| A | { int check, intert;
string cmdString = "dbo.FacultyCourse";
SqlCommand sqlCommand = new SqlCommand();
InitCheckInfo();
check = CheckCourseInfo();
if (check == 0) {
sqlCommand.Connection = loginForm.Connection;
sqlCommand.CommandType = CommandType.StoredProcedure;
sqlCommand.CommandText = cmdString;
sqlCommand.Parameters.Add(ref sqlCommand);
intert = sqlCommand.ExecuteNonQuery();
sqlCommand.Dispose();
if (insert == 0) {
MessageBox.Show("The data insertion is failed");
} else {
ClearCourse();
cmdInsert.Enabled = false; // clean up all course information
}
} | |
| I | else {
MessageBox.Show("Fill all Course information box, enter a NULL for blank column");
} |

FIGURE 6.44 The codes for the insert click method.

+   H. Otherwise, this data insertion is successful. The information stored in all TextBoxes is cleaned up to make it ready for users to perform a check or a validation for that data insertion. In addition, the insert button is disabled to avoid multiple insertions of the same data into the database.
I. If the returned check value is not zero, which means that TextBoxes are empty, a warning message is displayed to remind users to fill them immediately.

The detailed codes for the user-defined InsertParameters() are shown in Figure 6.45. The function of this code is straightforward and needs no further explanations.
Now we have finished coding jobs for this data insertion operation.
Let's run the project to test the new data insertion using the stored procedure method. Click on the Start to run the project, the suitable username and password as henry and then

| RTOInsertSP Project | InsertParameters(ref SqlCommand cmd) |
|---|---|
| private void InsertParameters(ref SqlCommand cmd) { |
| { cmd.Parameters.Add("FullName", SqlDbType.Char).Value = ComboName.Text;
cmd.Parameters.Add("CourseID", SqlDbType.Char).Value = xtCourseID.Text;
cmd.Parameters.Add("Course", SqlDbType.Char).Value = xtCourseName.Text;
cmd.Parameters.Add("Schedule", SqlDbType.Char).Value = xtSchedule.Text;
cmd.Parameters.Add("Classroom", SqlDbType.Char).Value = txtClassRoom.Text;
cmd.Parameters.Add("Credit", SqlDbType.Char).Value = txtCredits.Text;
cmd.Parameters.Add("Enroll", SqlDbType.Char).Value = xtEnroll.Text;
} } |

FIGURE 6.45 The codes for the method InsertParameters().