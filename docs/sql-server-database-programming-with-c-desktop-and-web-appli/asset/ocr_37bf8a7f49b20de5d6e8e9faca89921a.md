# Data Selection Query with Visual#.NET

Let's see how this piece of code works.

+   A. The System.IO namespace is enabled to use a method, MemoryStream(), to convert the column whose data type is byte[] in the Faculty table to the System.Drawing. Image that can be accepted and displayed in the PhotoBox in our Form for a selected faculty image.

+   B. Then the default Fill() method of the facultyTableAdapter is used to load data from the Faculty table into the DataSet. Since LINQ is applied with a DataSet and the DataSet must contain the valid data in all tables before this can be implemented.

+   C. A typical LINQ query structure is constructed and executed to retrieve all information for the selected faculty. The facultyQuery is a implicitly typed local variable with a data type var. The C# will be automatically convert var to any other data type. In fact

+   D. A foreach loop is used to pick up each column from the selected data row Row, which is obtained from the facultyinfo get the above LINQ query.

+   E. Assign each column to the selected TextBox to display them in the Faculty Form window.
F. Finally we need to call a system method MemoryStream() with an argument, which is a new object of the class MemoryStream(), embedded with our image in the Faculty table with an argument, to convert the latter from byte[] to a System.Drawing Image type. The latter can be accepted and displayed in the PhotoBox in our Form for a selected faculty.

At this point, we complete the code process for this Form. Do not forget to remove the comment for the LINQ clause in the codes shown in Figure 5.56 we have finished building of that. Now we can run and test our project.

Click the Build | Solution method to build and link our project, and click the Start button to run the project. Enter ybi as the username and come as the password on Login
Click on the Login button to open the Selection Form window, select the Faculty Information Name, and click the OK button to open the Faculty Form. Select Ying Bai from the Faculty Name ComboBox, and click the Select. All information related to this with a selected faculty image will be displayed, as shown in Figure 5.59.

You can select each TableAdapter or LINQ or DataSet by the Query Method Combo to perform different queries by different faculty members to confirm the correctness of our process.

At this point, we complete the query process for our Faculty table via the Faculty Form. Next we will take of data query for our Course via the Course Form.

# 5.12 BINDING DATA TO ASSOCIATED COURSES IN THE COURSE FORM

The functions of this form are illustrated by the following operational steps:

+   1) This Form allows users to find the course by the selected faculty from the Faculty Name TextBox control when users clicks the Select button. All queried courses (exactly all course_id) are displayed in the Course List.

+   2) The detailed information for each course, such as the course ID, course title, course schedule, classrooms and enrollment, can be obtained by clicking the desired course_id from the ListBox, and displayed in six TextBox controls.

+   3) The Back button allows users to return to the Selection Form to make other selection or obtain desired information related to that selection.