
## ADVANCED

- 8. JM Sales employs eight salespeople. The sales manager wants an application that allows him to enter a bonus rate. The application should use the rate, along with the eight sale amounts stored in an array, to calculate each salesperson's bonus amount. It also should calculate the total bonus paid to the salespeople. The application should display each salesperson's number (1 through 8) and bonus amount, as well as the total bonus paid, in the interface. Figure 19-20 shows a sample run of the application.
    - a. List the output and input items, as well as any processing items, then create an appropriate algorithm using pseudocode.
    - b. Create a new Visual Basic Windows application. Name the solution, project, and form file JM Sales Solution, JM Sales Project, and frmMain.vb, respectively. Save the application in the ClearlyVB\Chap19 folder. If necessary, change the form's name to frmMain.
    - c. Create the interface shown in Figure 19-20. The txtReport control's Font property is set to Courier New 10 point. Its Multiline and ReadOnly properties are set to True, and its ScrollBars property is set to Vertical.
    - d. Code the application. Use a one-dimensional array whose elements are initialized to the following sale amounts: 2400, 1500, 1600, 2790, 1000, 6300, 1300, and 2700. The txtRate control should accept only numbers, the period, and the Backspace key. The contents of the txtReport control should be cleared when a change is made to the contents of the txtRate control.
    - e. Save the solution, then start the application. Enter .1 as the bonus rate, then click the Create Report button. The interface should appear as shown in Figure 19-20. Test the application using your own data. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_458_0.png)

Figure 19-20: Sample run of the JM Sales application

- 9. In this exercise, you create an application that displays the highest and lowest values stored in an array.
    - a. Open the HighLow Solution, which is contained in the ClearlyVB\Chap19\HighLow Solution folder. Open the designer window, then open the Code Editor window.
    - b. Locate the btnHighest control’s Click event procedure. First, the procedure should sort the test scores to determine the highest score stored in the array. It then should count the number of students earning that score. Display the highest score, as well as the number of students earning that score, in the interface. Code the procedure. Save the solution, then start and test the application. Stop the application.
    - c. Locate the btnLowest control’s Click event procedure. The procedure should determine the lowest score in the array without sorting the array. (Hint: Assign the first score to a variable, then compare the remaining array values with that score.) The procedure also should count the number of students earning that score. Display the lowest score, as well as the number of students earning that score, in the interface. Code the procedure. Save the solution, then start and test the application. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_459_0.png)

- 10. Open the FigureThisOut Solution (FigureThisOut Solution.sln) file, which is contained in the ClearlyVB\Chap19\FigureThisOut Solution folder.
    - a. Open the Code Editor window and study the existing code. Start the application. Click the Find a Letter button. Type the letter a and press Enter. The message “A is in array element 0” appears in the interface. Test the application using the letters b, c, and d. The messages “B is in array element 1”, “C is in array element 2”, and “D is not in the array” will appear in the interface. Stop the application.
    - b. Change the Do clause to `Do Until strLetters(intSubscript) = strSearchFor OrElse intSubscript = strLetters.Length`. Save the solution, then start the application. Click the Find a Letter button. Type the letter a and press Enter. The message “A is in array element 0” appears in the interface. Test the application using the letters b and c. The messages “B is in array element 1” and “C is in array element 2” will appear in the interface. Click the Find a Letter button, then type the letter d and press Enter. A runtime error occurs. Click Debug on the menu bar, then click Stop Debugging.
    - c. Why does a runtime error occur when the Do clause is `Do Until strLetters(intSubscript) = strSearchFor OrElse intSubscript = strLetters.Length`, but not when it is `Do Until intSubscript = strLetters.Length OrElse strLetters(intSubscript) = strSearchFor`?
    - d. Change the Do clause to `Do Until intSubscript = strLetters.Length OrElse strLetters(intSubscript) = strSearchFor`. Save the solution, then start and test the application to verify that it is working correctly. Stop the application. Close the Code Editor window, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_459_1.png)

- 11. In this exercise, you find an error in an application’s code. Open the SwatTheBugs Solution (SwatTheBugs Solution.sln) file, which is contained in the ClearlyVB\Chap19\SwatTheBugs Solution folder. Open the Code Editor window and study the existing code. Start and then test the application. Notice that the application is not working correctly. Stop the application. Locate and correct any errors in the code. Save the solution, then start and test the application again. Stop the application, then close the solution.

## ANSWERS TO “TRY THIS” EXERCISES

- 1. See Figure 19-21.

```vb
Private Sub btnVerify_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnVerify.Click
    ' searches the array for the name of a guest, then displays
    ' an appropriate message

    Dim strPartyList() As String = {"Jacob", "Karen", "Gregory", _
                                    "Jerome", "Susan", "Michele", _
                                    "Heather", "Jennifer", "George"}

    Dim strSearchFor As String
    Dim intSubscript As Integer
    Dim strFound As String

    strSearchFor = txtGuest.Text.ToUpper

    intSubscript = 0
    strFound = "N"
    Do While strFound <> "Y" AndAlso intSubscript < strPartyList.Length
        If strPartyList(intSubscript).ToUpper = strSearchFor Then
            strFound = "Y"
        Else
            intSubscript = intSubscript + 1
        End If
    Loop

    If strFound = "Y" Then
        MessageBox.Show(strSearchFor & " is invited.", _
                        "Party List", MessageBoxButtons.OK, _
                        MessageBoxIcon.Information)
    Else
        MessageBox.Show(strSearchFor & " is not invited.", _
                        "Party List", MessageBoxButtons.OK, _
                        MessageBoxIcon.Information)
    End If
End Sub
```

Figure 19-21

- 2. See Figure 19-22.

```vb
Private Sub btnCount_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnCount.Click
    ' searches the array for a letter grade, then displays the
    ' number of times the letter grade appears in the array

    Dim strGrades() As String = {"C", "B", "C", "A", "B", "A", _
                                "F", "A", "B", "B", "C"}

    Dim strSearchFor As String
    Dim intCounter As Integer   ' counter

    strSearchFor = txtLetterGrade.Text.ToUpper
    intCounter = 0

    For intSubscript As Integer = 0 To strGrades.Length - 1
        If strGrades(intSubscript) = strSearchFor Then
            intCounter = intCounter + 1
        End If
    Next intSubscript

    MessageBox.Show(strSearchFor & ": " & intCounter.ToString, _
                    "Grades", MessageBoxButtons.OK, _
                    MessageBoxIcon.Information)
End Sub
```

**Figure 19-22**

## 20 Parallel and Dynamic Universes

**After studying Chapter 20, you should be able to:**

- Create parallel one-dimensional arrays
- Declare a module-level variable
- Declare a module-level array
- Utilize a dynamic one-dimensional array
