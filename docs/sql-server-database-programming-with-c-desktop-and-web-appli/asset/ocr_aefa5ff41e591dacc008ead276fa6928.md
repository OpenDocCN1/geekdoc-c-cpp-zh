# SQL Server Database Programming with C#

+   9) Remove the contents for all rows under the last row, image, and your finished query builder wizard should match one that is shown in Figure 7.3.
10) Click on the OK button to go to the next wizard. Remove the SELECT statement under the WHERE clause since we do not need this function. Click on the Next button to confirm this query and continue to the next step.
11) Modify the query function name from the default one to the UpdateFaculty and click on the Next button to go to the last wizard.
12) Click on the Finish button to complete this Query Builder and close the wizard.

Perform the following operations to build the data-querying:

+   1) Open the Data Source window and the TableAdapter Query Configuration Wizard by right-clicking on any place inside the Data Source window, and select the Edit DataSet with Designer from the popup menu.
2) On the opened wizard, go to the Faculty table, right-click on the last item in the Faculty table, and select Add Query item from the popup menu.
3) Keep the default selection, Use SQL statements, unchanged and click on the Next button to go to the next wizard.
4) Select and choose the DELETE item from this wizard since we need to be performing deleting query. Click on the Next button to continue to the next wizard.
5) Click on the Query Builder button we want to build our deleting query. The opened Query Builder wizard is shown in Figure 7.4.
6) Delete the whole line of the row faculty_id and the row @IsNull_faculty_name. Remove the contents of the columns Filter and Or for the faculty_name row.
7) Enter a question mark (?) into the Filter column alongside the faculty_name row and press the Enter key on the keyboard.

![](bbox=[0.18015, 0.553, 0.819, 0.897])

FIGURE 7.4 The delete query builder.