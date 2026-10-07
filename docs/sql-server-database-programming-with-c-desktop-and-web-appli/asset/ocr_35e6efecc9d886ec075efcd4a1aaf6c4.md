# Access Data in ASP.NET

![](bbox=[0.11, 0.08, 0.89, 0.28])

**FIGURE 8.96** The codes for the stored procedure deleteStudent().

The codes for this stored are straightforward and easily understood. If first input parameter, **sName**, a student name selected by the user, is declared. Then a local variable **sID** is generated since we need to delete a student's record based on the **student_id**, not **student_name**. An internal query is performed to get the matched **student_id** based on the student's name. Finally the student's record is deleted from the **Student** table.

Refer to 8.9.1 to add these two stored procedures into our DataContext class to enable the latter to recognize and use them. Next let's the codes to call stored procedures to perform data updating and deleting actions.

# 8.9.2 The Coding for the Data Upating Query

Open our project **WebSP_Student Project** and double-click on the **Update** button from the Design View of the page to open its click method, and enter the code shown in Figure 8.97 into that method.

Let's have a look at that piece of codes to see how it works. array declared first since we need to update a student image with this data updating action.

| WebSP_Student Project | cmdUpdate_Click(object sender, EventArgs) | |
|---|---||
| A | protected void cmdUpdate_Click(object sender, EventArgs) { |
| B | byte[] bImage; |
| | if (FileUploadImage.HasFile) |
| | Response.Write("<script>alert('An updating image using FileUpload!')</script>"); |
| | else { |
| C | bImage = getStudentImage(); |
| D | csep_updateStudentSP(txtStudentName.Text, Convert.ToDouble(txtGPA.Text), | | |
| | Convert.ToInt16(txtCredits.Text), txtMajor.Text, txtSchool.Text, txtEmail.Text, bImage, |
| | txtStudentID.Text); |
| E | CurrentStudent(); |
| F | ClearStudent(); |
| | } |

**FIGURE 8.97** The codes for the update button's click method.