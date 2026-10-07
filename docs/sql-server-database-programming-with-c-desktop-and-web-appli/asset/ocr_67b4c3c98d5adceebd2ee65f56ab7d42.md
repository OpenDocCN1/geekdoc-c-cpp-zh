# Data Selection Query with Visual C#.NET

![](bbox=[0.118, 0.085, 0.876, 0.278])

FIGURE 5.93 The testing result of our first stored procedure.

![](bbox=[0.118, 0.365, 0.876, 0.645])

FIGURE 5.94 The testing result for our second stored procedure.

In total, there is one row with eight columns returned: student_id, student_name, credits, gpa, major, schoolYear, and simage.

In a similar way, we can run our second stored procedure. You need to use a student_id as the input parameter to run it. Of course, you can use the student_id obtained from our first stored procedure, which is 177856. The testing result for our second stored procedure StudentCourseInfo is in Figure 5.94.

Now that our two procedures have been successfully tested, it is for us to develop a new Visual C# 2022 project SPSelect Project to call the two stored procedures to perform data query from the Student table in sample database.

# 5.16.4 Create a New Visual C# Project SPSelect Project to Query Student TABLE

We can create a brand new C# project to perform these data queries via our two stored procedures. However, in order to save time and space, we prefer to modify one of our projects,