# ASP.NET Web Services

| WinClickInsertPoint | cmdSelect_Click(object sender, EventArgs e) |
|---|---|
| private void cmdSelect_Click(object sender, EventArgs e) |
| { |
| WS_SQLInsert.SQLInsertResult = new WS_SQLInsert.SQLInsertRecord();
| WS_SQLInsert.WebServiceInsert = new WS_SQLInsert.WebServiceInsert();
| if (ComboBox.Text == "Stored Procedure") |
| try { wsSQLResult = wsSQLInsert.GetClassName(ComboBox.Text); }
| catch (Exception err) { MessageBox.Show("Web service is wrong: " + err.Message); }
| if (wsSQLResult == SQLInsertOK) |
| MessageBox.Show(wsSQLResult,"SQLInsertError");
| ProcessObject(wsSQLResult);
| } else |
| if (dsFlag == false) |
| MessageBox.Show("No DataSet Insert, do data insertion first");
| FullCourseDataSet(ref wsSQLResult);
| dsFlag = false;
| } |

**FIGURE 9.76** codes for the select button click method.

the Web service and it contains all course_id retrieved from the database, and it is assigned to our local instance to be processed later. An error message is displayed if any error were encountered during the execution of that Web method

C. In addition to our error-checking process by the system by inspecting the status of the data SQLInsertOK. The error source will be displayed if any error occurred.

D. If that Web method works, a user defined ProcessObject(), whose detailed codes are shown in Figure 9.77, it is called to extract all columns from that returned instance wsSQLResult.

E. If the user selects the DataSet Method, first we need to check whether the Web method InsertDataSet() has executed or by checking the status of the class-level variable dsFlag. Because a new course record should have been inserted into the database by using the method InsertDataSet() in the Insert button method. In this fact, that method performs both data insertion and data retrieval. An error may be encountered if you use this method to retrieve the information from the Select click method without first performing the data insertion from the Insert button click method since nothing has been inserted. Therefore nothing can be obtained from the returned DataSet. If this dsFlag is False, which means that nothing has been inserted, an information message is displayed to ask you to first perform the data insertion.

F. If the Web method InsertDataSet() has been executed, a user-defined method FullCourseDataSet(), whose detailed codes are shown in Figure 9.78, is called to fill the list box with all retrieved course_id.

G. Finally, the dsFlag resets to False to indicate that the method InsertDataSet() has not been executed.

The detailed codes for the methods ProcessObject() and FullCourseListBox() are shown in Figure 9.77. Let’s have a look at the codes in these two subroutines to see how they work.