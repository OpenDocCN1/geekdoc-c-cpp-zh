
# WinClientInsert Project

| | cmdlInsert_Click(object sender, EventArgs args) |
|---|---|
| A | private void cmdlInsert_Click(object sender, EventArgs args) { |
| B | int intInsert; intInsert = CheckSourceInsert(); WS_SQLInsert.WebServiceInsert wSQLInsert = new WS_SQLInsert.WebServiceInsert(); |
| C | if (intInsert == 0) { |
| D | if (ComboMethod.Text == "Stored Procedure Method") { try { |
| E | wSQLInsert.Result = wSQLInsert.SetInsertDataSet(ComboMethod.Text, txtCourseID.Text, txtCourseName.Text, Convert.ToInt32(txtCourse.Text), txtRoom.Text, txtSchedule.Text, Convert.ToInt32(txtEnroll.Text)); } catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); } if (wSQLInsert.ResultOK == false) MessageBox.Show(wSQLInsert.ResultError); |
| G | } else { |
| H | dsFlag = true; //indicate the DataSet is performed try { |
| I | wDataSet = wSQLInsert.InsertDataSet(ComboName.Text, txtCourseID.Text, CourseName.Text, txtSchedule.Text, txtRoom.Text, Convert.ToInt32(txtEnroll.Text), Convert.ToInt32(txtEnroll.Text)); } catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); } |
| J | cmdlInsert.Enabled = false; | } else { |
| | MessageBox.Show("Enter valid course information for all textboxes"); | } |

Figure 9.72 The codes for insert button click.

a new course record. If this happened, a message is displayed to direct the users to execute this method to insert a new course into the database. Another Try-Catch block is used to call the method InsertDataSet() with seven pieces of new course information as arguments to insert a new course record into the database. In addition to the new course insertion, this method performs a data query to retrieve all courses, including the newly inserted course, from the database and assign them to the DataSet that is returned to our client object.

H. If any running error is detected by the Catch statement, the error message is displayed.

I. Finally, the insert button is disabled to avoid multiple insertions of the record into the database.

J. If the returned value from calling the method CheckCourse() is zero, which means that not all course information has been entered into the related textbox, a warning message is displayed to remind the user to fill all required course to all textboxes.

The codes for the user-defined method CheckCourse() are shown in Figure 9.73.

Let's have a look at these codes to see how it works.

- Two integer variables, index and ret, are declared first. The former was as a loop counter and the latter as a returned status for this method. The ret is initialized to a non-zero value as to make this checking easy, a textbox array, tCourse[], is used to store all six textboxes in this method.

# ASP.NET Web Services

| WinClientInsert Project | CheckCourse() |
|---|---|
| private int CheckCourse() | |
| A int index, ret = 1; | |
| B TextBox[] tCourse = { txtCourse, txtName, txtCredits, txtClassRoom, txtSchedule, txtEnroll }; | |
| for (index = 0; index < tCourse.Length; index++) { |
| C if (tCourse[index].Text == null) { |
| ret = 0; |
| } | return ret; |

FIGURE 9.73 The codes for the user-defined method CheckCourse().

- B. A loop is executed to check whether any textbox is empty. If it is, the returned variable ret is cleared to 0.
- C. Otherwise, a successful value of 1 is returned to indicate that this data insertion checking is fine.

Another coding development is for the Course ID textbox, exactly to the TextChanged event of the Course ID textbox and combobox, ComboMethod, exactly to the SelectedChanged event. As mentioned, the Insert button should be disabled after one new course record has been inserted into the database to allow the multi-insertion of the same data. However, this button should be enabled when a new different course record is ready to be inserted into the database. As soon as the Course ID textbox changed or the Insert method is changed, which when a new record is ready and the Insert button should be enabled. To do these, double click on the Course ID and combobox ComboMethod from the Design View of our WinClient Form to open both TextChanged and SelectedChanged event triggering methods. Enter the following codes into these two events:

```cs
cmdInsert.Enabled = true;
```

At this point, we have finished all coding developments for the data insertion process. Before we can continue to develop the rest of our project, we prefer to run the client project to test this data insertion function.

The prerequisite to run our client project is to make sure that our Web service is in the running status in this local computer. To check and confirm, open our Web service WebInsertProject and click on the IIS button to run it. Then you may minimize our Web service by clicking on the Minimize button (make sure that Web service is in the running status even when the page is disappeared).

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status.

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. 

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. 

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. 

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. 

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. 

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. 

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status.  following operations.

Now you should find that a small white icon has been added to the status bar at the bottom of the screen. This small white icon means that our Web service is in the running status. operations.

# SQL Server Database Programming with C#

| Controls | Input Parameters |
|---|---|
| Method | Stored Procedure Method |
| Faculty Name | Ying Bai |
| Course ID | CSE-668 |
| Course Name | Introduction to Neural Networks |
| Schedule | T-H: 9:30-10:45 |
| Classroom | MTC-348 |
| Credits | 3 |
| Enrollment | 30 |

**FIGURE 9.74** The first course record to be inserted.

| Controls | Input Parameters |
| Method | DataSet Method |
| Faculty Name | Ying Bai |
| Course ID | CSE-526 |
| Course Name | Embedded Microcontrollers |
| Schedule | W-F: 9:00-9:55 AM |
| Classroom | MTC-308 |
| Credits | 3 |
| Enrollment | 32 |

**FIGURE 9.75** The second course record to be inserted.

## 9.4.3. Develop the Codes to Perform the Insert Validation

To confirm or validate a data insertion action, we can open our database and data table to check. However, a professional will do that is that we use codes to perform this validation. In this section, we discuss how to perform this validation by developing the codes in the **Select** button's click method in our client project.

As mentioned in the previous sections, this **Select** button is clicked after a new course insertion, all the new **course_id** will be retrieved from the database and displayed in a ListBox in this **CourseForm** window. This validation is also divided into two parts according to either the **Stored Procedure Method** or the **DataSet Method**. Different processes will be performed based on these methods. Because of the coding similarity between these two methods, we combine these codes and put them into this **Select** button's click method.

Double-click on the **Select** button from the Design View of Our **WinForm** Content.cs to open the click method and enter the codes that are shown in Figure 9.76 into this method. Let's take a closer look at how it works.

- A. A first instance of our derived class SQLInsertRecord, **wsSQLResult**, is re-declared since we declared this instance as a class variable before our base class SQLInsertBase. Also another instance of our Web service or proxy class is created and this instance works as a bridge to connect our client project with the Web methods developed in our web service method.

- B. If the **Stored Procedure Method** is selected by the user, a **Try-Catch** block is used to call our method **GetInsert()** with the selected faculty name as the input to retrieve all **course_id** from the database. This method returns an instance of our derived class defined in
