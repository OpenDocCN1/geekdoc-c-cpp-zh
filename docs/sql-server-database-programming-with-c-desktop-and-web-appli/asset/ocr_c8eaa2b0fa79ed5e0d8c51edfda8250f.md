# SQL Server Database Programming with C#

Click on the OK button to close this dialog box.
Do not forget to establish the cascaded relationship for Delete Rule and Update Rule items by expanding the Table Designer and the INSERT AND UPDATE Specifications, respectively. Click the Close button to finish the Foreign Keys Relationships dialog box when these relationships are done.

Go to the File | Save Login item to save this relationship. Click Yes for the following dialog box to finish. Now right-click on the Keys folder under the dbo.Login table, and select Refresh item to show our new created foreign key FK_Login_Student.

# 2.9.4.3 Create Relationship between the Faculty and the Course Tables

The relationship between the Faculty and the Course tables is one-to-many, the faculty_id in the Faculty table is a Primary key and the faculty_id in the Course is a

On the opened Foreign Keys Relationships dialog, change the name of this new relationship to FK_Course_Faculty in the (Name) box under the Identity item on the right-hand side. Expand the Tables and Columns Specifications item and click on the three-dot button on the right to open the Tables and Columns dialog box.

In the opened Tables and Columns dialog box, select the Faculty table from the Primary key table combobox and select the faculty_id from the box that is just under the Foreign key table combobox. Your finished Tables and Columns dialog should match one that is in Figure 2.43.

Click on the OK button to close this dialog and setup the cascaded relationship for the Delete Rule and Update Rule items. Then click the Close button to finish the Foreign Keys Relationships dialog box. Go to the File | Save Course item and click Yes for the Message Box to save this setting.

Now right-click on the Keys folder under the dbo.Course table, and select the Refresh item. Immediately you can find our new created relationship key FK_Course_Faculty.

| Tables and Columns | |
|---||
| Relationship name: | |
| FK_Course_Faculty | |
| Primary key table: | Foreign key table: |
| Faculty | Course |
| faculty_id | faculty_id |

![](bbox=[0.118, 0.917, 0.506, 0.931])