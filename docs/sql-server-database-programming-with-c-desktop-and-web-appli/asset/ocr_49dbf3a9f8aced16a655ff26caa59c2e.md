# Access Data in ASP.NET

select one to get the course information as the project runs. Here a potential bug exists for this piece of codes. As mentioned in Section 8.4.9.1, an AutoPostBack property will be set to true when the user clicked and selected an item from the list control, and this property will be sent back to the server to indicate that an action has been taken by the user to this list. After the server received this property, it will send back a refreshed Page to the client; therefore, the Page_load will run again a refreshed Course page is sent. The result of execution of this Page_load is to attach copy of all faculty members to the end of those members that have been added into the combobox ComboName when the user clicked the CourseList box increases, the number of faculty members will also be increased and displayed in the ComboName box. To avoid this duplication, you need to add all members to the first time as the Course page occurred, but nothing if any other AutoPostBack property occurred.

The coding for Back button method is similar to that for the Back button in the Faculty page. When this is clicked the page switched to the Selection page. The Redirect() of the server Response object is used to fulfill this switching back function. Double click the Back button on the Design View of the Course page and enter the following codes into this:

```
Response.Redirect("Selection.aspx");
```

Next let's continue to do the coding for the Select button's method.

# 8.4.9.4 Coding for the Select Click Method

As mentioned at the beginning of this section, the function of this is: when the user selected a desired faculty from the Family Name and clicks the Select button, all course_id to courses taught by the faculty should be retrieved from the database and displayed in the list control Courselist on the Course page.

Double-click on the Select button from the Design View of the Course page window to open its List Click method, and the codes that are shown in Figure 8.30 into this.

| SQLSelectProject | cmdSelect_Click(object sender, EventArgs e) | |
|---|---||
| A | protected void cmdSelect_Click(object sender, EventArgs e) { |
| B | string strCourse = "SELECT course_id FROM Course JOIN Faculty"; |
| C | strCourse += "WHERE Course.faculty_id = Faculty.faculty_id AND Faculty.faculty_name = @name"; |
| D | SqlCommand sqlCommand = new SqlCommand(strCourse, sqlConnection); |
| E | sqlCommand.CommandType = SqlCommandType.Text; |
| F | sqlCommand.Parameters.Add("@name", SqlDbType.Char).Value = ComboName.Text; |
| G | SqlDataReader dataReader = sqlCommand.ExecuteReader(); |
| H | if (dataReader.HasRows) { |
| I | FillCourse(dataReader); |
| J | else |
| K | Response.Write("<script>alert('No matched course found!')</script>"); |
| L | dataReader.Close(); |
| M | sqlCommand.Dispose(); |
| } |

Figure 8.30 The codes for the select button's method.