
# SQL Server Database Programming with C#

RTOSelectProject, which we built in the previous section to reduce our working loads. Perform the following operations to complete this solution-project- copying-pasting and modification process:

- 1. Open the Windows explorer window and browse our solution folder RTOSelect Solution. One can find this and the project from the CRC Press tip in a folder `Class DB Projects\Chapter 5` that is under the Students folder in that site.
2. Right-clicking on that folder and select the Copy item to copy that folder, then go to your local machine and verify your desired folder, right click on that folder and select the Paste item to paste into your local folder.
3. Expand that copied solution folder and change the name to PSelect Solution and the project name to PSelect Project, respectively.
4. Open the executed file via Notepad under the renamed project PSelect Project folder.
5. On the opened file, go to the <RootNamespace> (line 9) and <AssemblyName> tags, change the RootNamespace to PSelect_Project and the AssemblyName to PSelect Project, respectively.
6. On the same file, go to the <StartObject> tag (line 36), and change its name to PSelect_Project.Program.
7. Go to the File | Save menu to edit the saved file and close this.
8. In the Windows explorer window, change the name of that saved file to PSelect_Project.csproj.
9. Double-click on renamed file, PSelect.Project.csproj, to open this project.
10. Go to the Solution explorer, window-right-click to the Login-click on the Login.cs and select the View Code item to open its code. Change its namespace to PSelect_Project.
11. In the Solution explorer, expand the Login.cs folder and double-click on the Login.designer.cs. Change its name on the top to PSelect_Project.
12. Repeat steps 10 and 11 for all other files, Course.cs, Faculty.cs, Selection.cs and Student.cs, change their names to PSelect_Project.
13. In the Solution explorer, double-click on the C# Program.cs file to open it, and change its namespace to PSelect_Project.
14. Now go to the Build | Build Solution item to build our project to complete this copy-paste process.

Next let's start our coding process for the Student Form window. First let's build the codes for the constructor of this Student class.
Go to the Solution explorer, right-click on the Student.cs folder and select the View Code item to open its code. Enter the codes shown in Figure 5.95 into its constructor. Let's have a closer look at this piece of codes to see how it works.

- A. System.Data.SqlClient member is added first since we need to use a group of data components that are SQL Data Provider-dependent under that namespace in this section.
- B. A New InfoObject, login, is declared and the purpose of generating this new object is to set up a valid connection to our sample database to get a connection object we need to use query data from the Student table.
- C. All five student members are added to the Student Name combobox to enable users to select one of them to perform data query for that selected student. The SelectedIndex = 0 makes the first student in the Student Name combobox as a default.
- D. Two query methods, DataAdapter Method and DataReader Method, are added to the Query Method combobox to enable users to select one to perform the related data query. Similarly, the first query method is selected as the default method by setting the SelectedIndex property

# Data Selection Query with Visual#.NET

| SPSelect Project | StudentForm() |
| :--- | :--- |
| A | `using System.Data; using System.Data.SqlClient; using System.Data.OleDb; using System.Drawing; using System.Linq; using System.Text; using System.Windows.Forms; namespace SPSelect_Project { public partial class StudentForm : Form { LoginForm logInForm = new LogForm(); public StudentForm() { InitializeComponent(); ComboName.Items.Add("Tom Erica"); ComboName.Items.Add("Ashly Jade"); ComboName.Items.Add("Holes Smith"); ComboName.Items.Add("Andrew Woods"); ComboName.Items.Add("Blue Valley"); ComboName.SelectedIndex = 0; ComboName.Items.Add("DataAdapter Method"); ComboName.Items.Add("DataReader Method"); ComboName.SelectedIndex = 0; } }` |
| B C D | |

**FIGURE 5.95** The codes for the constructor of the student window.

- 0. A point to be noted that although two query methods are available to the users, both methods need to call our stored procedures to perform related queries to the *Student* table in our sample database.

Now open the Student Form by going to the Solution Explorer, and right-clicking on the *Student.cs* and select the **Designer** item.
Then open the **Select** Click method by double-clicking on the **Select** button from the Student Form, and enter the codes that are shown in Figure 5.96 into this method.
Let's take a closer look at this piece of codes to see how it works.

- A. Two stored procedures' names are assigned to two string variables, strStudent and strStudentCourse, The names must be declared identical to those we created in two stored procedures: `dbo.StoredInfo` and `dbo.StoredCourseInfo`.
- B. All data components are declared and created in the following section, which include two TableAdapters, two DataTypes, two Command objects and one Data.
- C. The user-defined method `SqlCommand` is called to initialize the first Command object with the correct Connection, CommandType and CommandText properties. In order to execute our stored procedure, the properties should be set as follows:
* `Connection = login.sqlConnection`
* `CommandType = CommandType.StoredProcedure`
* `CommandText = "dbo.StoredInfo"`
The content of the CommandText must be equal to the name of the stored procedure developed above.

# SQL Server Database Programming with C#

# SPSelectProject

```c
private void cmdSelect_Click(object sender, EventArgs e)
{
    string strStudent = "dbo.StudentInfo";
    string strCourse = "dbo.CourseInfo";
    SqlDataAdapter dataAdapter = new SqlDataAdapter();
    SqlDataAdapter studentCourseDataAdapter = new SqlDataAdapter();
    SqlCommand cmdStudent = new SqlCommand();
    SqlCommand cmdCourse = new SqlCommand();
    DataTable studentTable = new DataTable();
    DataTable courseTable = new DataTable();
    SqlDataReader studentReader;

    BuildCommand(cmdStudent, strStudent);
    cmdStudent.Parameters.Add("@StudentName", SqlDbType.Char).Value = ComboName.Text;
    cmdStudent.CommandText = "Select * from StudentTable";
    dataAdapter.Fill(studentTable);
    if (studentTable.Rows.Count > 0)
    {
        FillStudentTextBox(studentTable);
    }
    else
    {
        MessageBox("No matched student found!");
        BuildCommand(cmdCourse, strCourse);
        cmdCourse.Parameters.Add("@StudentID", SqlDbType.Char).Value = txtStudentID.Text;
        cmdCourse.CommandText = "Select * from CourseTable";
        studentCourseDataAdapter.Fill(courseTable);
        if (courseTable.Rows.Count > 0)
        {
            FillCourseList(courseTable);
        }
        else
        {
            MessageBox("No matched course_id found!");
        }
    }
    cmdStudent.Dispose();
}

// DataReader Method
SqlCommand cmdStudent = new SqlCommand();
SqlDataReader studentReader = cmdStudent.ExecuteReader();
if (studentReader.HasRows == true)
{
    MessageBox("No matched student found!");
    studentReader.Close();
    BuildCommand(cmdCourse, dr, strCourse);
    cmdCourse.Parameters.Add("@StudentID", SqlDbType.Char).Value = txtStudentID.Text;
    SqlDataReader courseReader = cmdCourse.ExecuteReader();
    if (courseReader.HasRows == true)
    {
        FillStudentReader(courseReader);
    }
    else
    {
        MessageBox("No matched course_id found!");
    }
    studentReader.Close();
    cmdCourse_dr.Dispose();
    courseReader.Close();
}

studentTable.Dispose();
courseTable.Dispose();
studentDataAdapter.Dispose();
studentCourseDataAdapter.Dispose();
cmdStudent.Dispose();
cmdCourse.Dispose();
}
```

FIGURE 5.96 The codes for the select button click.
