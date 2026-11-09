The numbers 2 through 6 appear in the interface. Stop the application, then close the solution. (If you need to recreate the numbers.txt file, open the file in a window in the IDE. Delete the contents of the file, if necessary, then type the numbers 1 through 5, pressing Enter after typing each number.)

ADVANCED

+   6. During July and August of each year, the Political Awareness Organization (PAO) sends a questionnaire to the voters in their district. The questionnaire asks the voter for his or her political party (Democratic, Republican, or Independent) and age. From the returned questionnaires, the organization’s secretary tabulates the number of Democrats, Republicans, and Independents in the district. The secretary wants an application that she can use to save each respondent’s information (political party and age) to a sequential access file. The application also should calculate and display the number of voters in each political party. Create a new Visual Basic Windows application. Name the solution, project, and form file PAO Solution, PAO Project, and frmMain.vb, respectively. Save the application in the ClearlyVB\Chap23 folder. If necessary, change the form’s name to frmMain. Create the interface shown in Figure 23-14. The Party text box should accept only the Backspace key and the letters D, d, R, r, I, or i. The Age text box should accept only numbers and the Backspace key. Code the Click event procedures for the Write to File and Display Totals buttons. Save the solution, then start and test the application. Stop the application, then close the solution.

![](bbox=[0.192, 0.52, 0.6, 0.729])

Figure 23-14: User interface for the PAO application

![](bbox=[0.124, 0.765, 0.196, 0.822])

+   7. Open the FigureThisOut Solution (FigureThisOut Solution.sln) file, which is contained in the ClearlyVB\Chap23\FigureThisOut Solution folder. Open the Code Editor window and study the existing code. Why does the true path in the btnWrite control’s Click event procedure open the sequential access file for output first, then close the file, and then open it for append? Start and test the application. Stop the application. Close the Code Editor window, then close the solution.