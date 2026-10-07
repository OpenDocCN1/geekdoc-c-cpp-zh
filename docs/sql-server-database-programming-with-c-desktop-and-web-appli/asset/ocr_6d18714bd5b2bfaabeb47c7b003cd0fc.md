# 198 SQL Server Database Programming with C#

![](bbox=[0.208, 0.081, 0.791, 0.566])

FIGURE 5.29 The finished connection wizard.

8) Now you can check on the Show the connection string checkbox if you like to keep and save this connection string in your project, as shown in Figure 5.30. We may need to use this connection string when we build our database application project with runtime object method later. Click on the Next to go to the next step.

9) In the next view, Save the Connection String to the Application Configuration File, keep the default settings and click on the Next to continue.

10) In the next view, Choose Your Database Objects, as shown in Figure 5.31, expand the Tables folder and select all of your five tables, Course, Faculty, Login, Student and StudentCourse, by checking all of them one by one. Also check the Views folder to enable us to check all of five tables in a View format later.

Your finished Your Database Objects wizard should match one that is shown in Figure 5.31. Click on the Finish to complete adding this data source process.

Immediately, you can find that a new instance of the Dataset, CSE DEPTDataSet, is added into your project, which is shown in Figure 5.32. Five data tables in this Dataset are only mappings or copies of those tables in real time. The setup between the project and the database is closed as this is finished. You will need to call some data query to reopen this connection as you perform data actions later in your project.