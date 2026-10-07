# 494 SQL Server Database Programming with C#

# 8.9.1.2 Add Two Stored Procedures into the DataContext Class

Prior to let the codes for the Select button, we need to add our stored procedures to the DataContext class, CSE_DEPT.dbml, built in Section 8.7 via the Object Relational Designer. Perform the following operations to add two stored procedures, dboStudentInfo and dboCourseInfo, into our DataContext class:

+   1) Double-click on our DataContext class CSE_DEPT.dbml from the Solution Explorer to open the Object Relational Designer, as shown in Figure 8.86.
2) Drag the first procedure, StudentInfo that is located under the Stored Procedures folder in the opened database in the Server Explorer and drop it into the second panel on the right (Creating Methods panel), as shown in Figure 8.86. The finished first procedure is displayed on that panel.
3) In a similar way, drag and drop the second stored procedure StudentCourseInfo to the method panel.
4) The finished adding two stored procedures into the method panel should match one that is shown in Figure 8.86.
5) Go to File Save All menu item to save those operations.

Now let's develop the codes for the Select button's click to query student records by calling two stored procedures via the LINQ to SQL technique.

# 8.9.1.3 The Coding for the Data Selection Query

The function of this click is: when the user selects a desired student from the Student Name combo box and clicks the Select button, a procedure dbo.StudentInfo built in Section 5.16.3, should be called to get all detailed information related to the student and displayed in text-boxes with a selected student image in the Student page. In addition to displaying detailed

![](bbox=[0.119, 0.555, 0.88, 0.903])

FIGURE 8.86 The two stored procedures as methods or functions.