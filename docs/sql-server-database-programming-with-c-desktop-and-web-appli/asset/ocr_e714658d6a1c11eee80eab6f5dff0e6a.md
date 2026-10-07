# SQL Server Database Programming with C#

Let's have a look at this piece of code to see how it works.

+   A. The joined table query string is declared at the beginning of this method. Here only one column or the first column, course_id, is queried. The reason for this is that we need to use this course_id, not course name, as the identifier to pick each course's detailed information from the Course table when the user clicked and selected that course_id from the CourseList box. The assignment operator = is used for the ON clause in the definition of the query string, and it is required by SQL Server database operation. For a more detailed discussion about the joined table query, refer to Section 5.15.1 in Chapter 5.
B. Some SQL data objects, as Command and DataReader, are created here. All of these objects are prefixed by the keyword sql to indicate that all components are related to the SQL Server database.
C. The SqlCommand object is initialized with the connection string, command type, command text and command parameter. The parameter's name must be identical with the dynamic nominal parameter @name, which is defined in the query string and is exactly located after the assignment operator in the ON clause. The parameter's value is the content of the Faculty name, which should be selected as the user runs results later.
D. The ExecuteReader() of the Command class is executed to read back all courses (course_id) by the selected faculty and assigns them to the DataReader.
E. If the HasRows property of the DataReader is true, which means at least one row has been retrieved from the database, the FillCourse() method to be built later is called to fill the CourseList box with all course_id.
F. Otherwise, this join query is failed and a warning message is displayed.
G. Finally some cleaning jobs are performed to release objects used for this query.

Now let's take care of the coding for the user-defined method FillCourseReader(), which is shown in Figure 8.31. Open the code page of the Course Web form and enter the codes that are shown in Figure 8.31 to create this method into the Course class.
Let's have a look at this piece of codes to see how it works.

+   A. A local variable strCourse and this variable can be considered as an intermediate variable holder that is used to temporarily hold the queried data row from the Course table.
B. The CourseList is cleaned up before it can be filled by the course_id.
C. A while() loop is utilized to retrieve the first column for each row by GetString(0), whose index is 0 and the value is the course_id. The data is first assigned to the intermediate variable strCourse, and then is added into the CourseList box by using the Add().

```
SQLWebSelect private void FillCourseReader(SqlDataReader CourseReader)
{
    string strCourse = string.Empty;
    CourseList.Items.Clear();
    while (CourseReader.Read())
    {
        strCourse = CourseReader.GetString(0); //the 1st column is course_id
        CourseList.Items.Add(strCourse);
    }
}
```

FIGURE 8.31 The coding for the method FillCourseReader.