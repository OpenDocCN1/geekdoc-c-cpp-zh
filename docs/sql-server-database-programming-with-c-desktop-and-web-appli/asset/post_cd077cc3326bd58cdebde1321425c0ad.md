
# 222
# SQL Server Database Programming with C#

| SelectWizard Project | cmdBack_Click(object sender, EventArgs e) |
|---|---|
| private void cmdBack_Click(object sender, EventArgs e) { \n  this.Hide(); \n } | |

FIGURE 5.57 The codes for the back button.

for this situation to require users to handle this problem. The user can continue to select correct faculty name or exit the project. If this property is non-zero, which indicates that this fill is successful and a matched faculty name is found and the Table in our Dataset has been filled. A record related to the matched faculty will be displayed in TextBoxes and a PictureBox.

D. Otherwise, the LINQ & DataSet Method is selected and a user-defined method LINQToDataSet() that will be developed below is called to retrieve the back information with a LINQ query method.

The codes for the Back button Click method are very simple. The Faculty Form will be hidden when this button is clicked. A Hide() method is used for this purpose, which is shown in Figure 5.57.

### 5.11.2 Develop Codes to Query Data Using the LINQ Method

The LINQ query technique is one of the most popular query methods and widely implemented in the modern database programming applications. The query process can be significantly integrated and improved using this technology. We have already provided a very detailed discussion about this technology in Chapter 4. Refer to that chapter to get a clear picture for this issue. In this part, we will concentrate on the implementations of this method.

Open the Code Window of the Faculty Form if it is not opened, a user-defined method and enter the codes, which are shown in Figure 5.58, into this method.

| SelectWizard Project | LINQToDataSet() |
|---|---|
| A; using System.LINQ; | |
| B { \n  this.facultyTableAdapter.Fill(cse_DeptDataSet.Faculty); \n  var facultyInfo = (from row in cse_DeptDataSet.Faculty \n  where row.Field("faculty_name").Equals(ComboBox.Text) \n  select row); \n  foreach (var row in facultyInfo) { \n  this.facultyID.Text = row.faculty_id; \n  this.facultyName.Text = row.faculty_name; \n  this.title.Text = row.title; \n  this.office.Text = row.office; \n  this.college.Text = row.college; \n  this.email.Text = row.email; \n  this.Photo.Image = Image.FromStream(new MemoryStream(row.Image)); \n}\n} | |

FIGURE 5.58 The detailed codes for the LINQ method.

## Data Selection Query with Visual#.NET

Let's see how this piece of code works.

- A. The System.IO namespace is enabled to use a method, MemoryStream(), to convert the column whose data type is byte[] in the Faculty table to the System.Drawing.Image that can be accepted and displayed in the PictureBox in our Form for a selected faculty image.
- B. Then the default Fill() method of the facultyTableAdapter is used to load data from the Faculty table into the DataSet. Since LINQ is applied with a DataSet and the DataSet must contain the valid data in all tables before this can be implemented.
- C. A typical LINQ query structure is constructed and executed to retrieve all information for the selected faculty. The facultyQuery is a implicitly typed local variable with a data type var. The C# will be automatically convert var to any other data type. In fact
- D. A foreach loop is used to pick up each column from the selected data row Row, which is obtained from the facultyinfo get the above LINQ query.
- E. Assign each column to the selected TextBox to display them in the Faculty Form window.
- F. Finally we need to call a system method MemoryStream() with an argument, which is a new object of the class MemoryStream(), embedded with our image in the Faculty table with an argument, to convert the latter from byte[] to a System.Drawing. Image type. The latter can be accepted and displayed in the PictureBox in our Form for a selected faculty.

At this point, we complete the code process for this Form. Do not forget to remove the comment for the LINQ clause in the codes shown in Figure 5.56 we have finished building of that. Now we can run and test our project.

Click the Build | Solution method to build our project, and click the Start button to run the project. Enter the username and password on Login. Click on the Login button to open the Selection Form, select the Faculty Name from the ComboBox, and click Select. All information related to the selected faculty will be displayed, as shown in Figure 5.59. You can select each TableAdapter or LINQ DataSet to perform different queries by different members to confirm the correctness of our process. At this point, we complete the query process for our Faculty table via the Faculty Form. Next we will take of the Course Form.

## 5.12 BINDING DATA TO ASSOCIATED COURSES IN THE COURSE FORM

The functions of this form are illustrated by the following steps:

- 1) This Form allows users to find the course by the selected faculty from the Faculty Name control when users clicks Select. All queried courses (course_id) are displayed in the List.
- 2) Detailed information for each course, such as the course ID, course title, course schedule and enrollment, can be obtained by clicking the desired course from the List, and displayed in TextBox controls.
- 3) The Back button allows users to return to the Selection Form to make other selection or obtain desired information related to that selection.

# SQL Server Database Programming with C#

img/d59a47501d0a20fc04a49c6fb7252_0.png
59 The running status of the faculty form window.

In this section, we only take care of two buttons: the Select and Back buttons. The coding for the Insert, Update and Delete buttons will be discussed in the following chapters. In step 1, queries need to be performed; in order to find the courses taught by the selected faculty, we need to obtain the faculty ID that is associated with the selected faculty from the Faculty Name when user clicks Select because the only available information in the Course table is the faculty_id. So we need to create a query that returns a single value (faculty_id) from the Faculty table; then we will create another query in the Course table to find the courses taught by the selected faculty based on the faculty_id obtained from the table. Now let's handle the first step, which is to create a query to obtain associated faculty_id from the selected faculty from the Faculty Name comboBox in the Course form.

Open the DataSet Designer and right-click on the last line of the faculty table and select Add Query to TableAdapter Configuration Wizard. Keep the default selection use SELECT statements and click on the Next button to get to the next. Check the radio button in front of SELECT which returns a single value to choose this query type, and click the Next button to get the next. Then click on the Query to build our query. Performing the following operations to complete this query building:

- 1) Click the first row (only one row) from the second select.
- 2) Double-click on the select and select Delete from the popup menu to delete this row.
- 3) Go to the top pane and select the faculty_id and faculty_name columns from the Faculty table by checking those columns.
- 4) Go to the second pane and uncheck the checkbox for the faculty_name column from the Output column since we do not want to use it as the output. Instead, we need to use it as a query criterion to filter this query.

img/d59a47501d0a20fc04a49c6fb7253_0.png
Figure 5.60 The finished query for the faculty_id.

- 5) In the second pane, right-click on the Group By column and select the Edit Item from the popup menu to remove this Group By.
- 6) Type a character '?' on the Filter column of the faculty_name row, and press the Enter key from the keyboard. Your finished Query Builder should match one that is shown in Figure 5.60.

The SQL statement shown in the text pane or the third pane is:

```
SELECT faculty_id FROM Faculty WHERE (faculty_name = @Param1)
```

Click on the OK button and the Next button for the next window to continue to the next wizard. Enter FacultyIdByName into the box as your function name and then click the Next and the Finish buttons to complete this query building.

Now letss build our second query to find the courses taught by the selected faculty from the table. Open the DataSet Designer to create our desired query and modify the (Fill) method for the CourseTableAdapter.

Open the Data Source by clicking the View | Other Windows | Data Sources menu from the menu bar. Then right-click on any item in that window and select Edit DataSet with Designer to open the DataSet Designer. Right-click on the last line of the Course table and choose the Add Query item to open the TableAdapter Query Configuration Wizard. Keep the default selections use SELECT statements and click on Next. Also keep the top selection SELECT which returns rows in the next window and click on Next. Then click the Query Builder button to open the wizard in Figure 5.61.

Keep the default selections for this graphical query. We only need the course_id column and will explain why we need to keep these default items later. Go to the Filter column along the faculty_id row, type a question mark and press the Enter key from the keyboard. This is equivalent to setting
