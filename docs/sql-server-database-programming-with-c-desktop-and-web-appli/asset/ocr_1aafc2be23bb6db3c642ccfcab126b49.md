# SQL Server Database Programming with C#

# RTOupdateDelete Project

```
private void Delete_Click(object sender, EventArgs e)
{
    string cmdString = "DELETE FROM CourseButtons.WHERE (course_id = @courseid)";
    MessageBoxButtons vbButton = MessageBoxButtons.YesNo;
    SqlCommand cmd = new SqlCommand(cmdString);
    DialogResult Answer;
    int intIndex;

    Answer = MessageBox.Show("Do you want to delete this record?", vbButton);
    if (Answer == DialogResult.Yes)
    {
        cmd.Connection = loginConnection;
        cmd.CommandType = CommandType.Text;
        cmd.CommandText = cmdString;
        cmd.Parameters.Add("@courseid", SqlDbType.Char).Value = txtCourseID.Text;
        intIndex = cmd.ExecuteNonQuery();
        cmd.Dispose();
        if (intIndex == 0)
        {
            MessageBox.Show("The Deleting is failed");
        }
        else
        {
            ClearCourse();
        }
    }
}

private void ClearCourse()
{
    int index;
    TextBox[] cbox = {txtCourseID, txtCourseName, txtSchedule, txtClassroom, txtCredits, txtEnroll};
    for (index = 0; index < cbox.Length; index++)
        cbox[index].Text = ""
}
```

FIGURE 7.27 The codes for the course-deleting query.

C. All data components and local variables used in this method are declared here. The data type of the variable Answer is DialogResult. However, one can use an integer variable to replace it. The variable intIndex is used to hold the return value from calling the ExecuteNonQuery() method to delete the record from the Course table.
D. As the Delete button is clicked when the project runs, first a MessageBox is displayed to confirm the user has selected the course from the Course table.
E. If the user's answer is Yes, the deleting operation begins to proceeds. The Command object is initialized and built using the Connection object and the Command string we defined at the beginning of this method.
F. The dynamic parameter @id is replaced by the real parameter, a course_id stored in the Course Listbox, Courselist.
G. The ExecuteNonQuery() method of the Command class is called to execute the data-deleting query to the table. The running count of calling is stored in the local variable intIndex.
H. The Command object is released after the delete.
I. The returned value from calling the ExecuteNonQuery() method is equal to the number of rows that have been successfully deleted from the Course table. If it returns zero, which means no row has been deleted from the table and this data deleting is failed, an error message is displayed if that situation occurred.
. Otherwise, the course data deleting action is executed successfully. After a data deleting action is completed, all course information stored in six TextBoxes should be cleaned up to enable users to check and confirm that data deleting action. This cleaning job can be done