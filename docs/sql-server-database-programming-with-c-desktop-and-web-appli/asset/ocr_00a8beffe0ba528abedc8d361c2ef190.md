# Data Selection Query with Visual C#.NET

**StudentName**, and the output @StudentID The latter must be indicated with the keyword OUTPUT. Later in the child stored procedure, you must declare this parameter as an output parameter using the keyword OUTPUT to match this definition in the main stored procedure.

+   E. After the child stored procedure is executed, it returns the student_id. Now we can perform our main query to obtain all courses taken by the selected student from the StudentCourse table based on the student_id returned by the child stored procedure.

+   F. The retrieved courses are returned to the child procedure developing in Visual C# project.

Now click on the **Update** item on the upper-left, as shown in Figure 5.108, to save this stored procedure. Click on the **Update Database** button on the opened **Preview Database** Updates to finish this saving.

Second's create our child stored procedure. Right click on the **Stored Procedures** folder in the Server explorer window of our sample **CSE_DEPT** has connected and select the **Add New Stored Procedure** item from the popup menu. On the opened wizard, enter the codes that are in Figure 5.109 into this child stored procedure.

The functionality for each coding line is outlined below:

+   A. The name of our child stored procedure is declared first, which is: dbo.StudentInfo. This name must be identical with the name used by our main stored procedure when this procedure is called.

+   B. Two parameters are declared here; the one, @sName, is the input, and the second, @sid is the output parameter. The default type of the parameter is INPUT, so the keyword OUTPUT must be attached for the second parameter since it is an output and will be returned to the main stored procedure.

+   C. The SQL statement is executed to get the desired student_id from the Student table based on the input name. The returned student_id will be assigned to the output parameter @sid by using the **SET command.

+   D. The output @sid is returned to the main stored procedure.

Now click on the **Update** item on the upper-left, as shown in Figure 5.109, to save this stored procedure. Click on the **Update Database** button on the opened **Preview Database** Updates to finish this saving.

To test both main and child stored procedure in the Server explorer window, right-click on the main stored procedure **StudentAndCourse** item, and select **Execute** to open the Run Stored Procedure.

![](bbox=[0.119, 0.712, 0.88, 0.903])

Figure 5.109 The child stored procedure.