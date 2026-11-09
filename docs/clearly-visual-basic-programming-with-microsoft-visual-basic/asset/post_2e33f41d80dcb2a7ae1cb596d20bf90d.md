
### To open the Weekly Pay application, and then test the application:

- 1. Start Visual Studio 2008 (or Visual Basic 2008 Express Edition). Open the **Weekly Pay Solution (Weekly Pay Solution.sln)** file, which is contained in the ClearlyVB\Chap17\Weekly Pay Solution folder. If necessary, open the designer window.

- 2. Start the application. Type **41** in the Hours box and then type **9** in the Rate box. Click the **Calculate** button. The Calculate button's Click event procedure calculates and displays the regular pay, overtime pay, and gross pay. See Figure 17-4.

![](img/cf88270932e011575089da06b940a1d9_390_0.png)

Figure 17-4: Interface showing the calculated amounts

- 3. Now change the number of hours from 41 to **4**, but don't click the Calculate button yet. Notice that the interface still shows the pay amounts for 41 hours; this is because the amounts aren't updated until you click the Calculate button. Click the **Calculate** button to update the pay amounts, then click the **Exit** button.

To avoid confusion, it would be better to remove the pay amounts from the interface whenever a change is made to either the number of hours in the txtHours control or the rate of pay in the txtRate control. You can do this by entering the three assignment statements lblRegular.Text = String.Empty, lblOvertime.Text = String.Empty, and lblGross.Text = String.Empty in each text box's **TextChanged event** procedure. A text box's **TextChanged event** occurs whenever a change is made to the contents of the text box. You also can remove the pay amounts by entering the assignment statements in a sub procedure, and then entering the appropriate **Call** statement in both **TextChanged** event procedures. You will use the latter approach, because entering the assignment statements in a sub procedure saves you from having to enter them more than once. In addition, if the application is modified—for example, if the user wants you to assign the string “N/A” rather than the empty string to the labels—you will need to make the change in only one place in the code.

### To enter the ClearLabels sub procedure and Call statements, and then test the application:

- 1. Open the Code Editor window. Click the **blank line** below the Public Class frmMain line, then press **Enter**. Enter the ClearLabels procedure shown in Figure 17-5.

![](img/cf88270932e011575089da06b940a1d9_391_0.png)

- 2. Open the code template for the txtHours control’s TextChanged event procedure. Type **Call ClearLabels()** and press **Enter**. Now open the code template for the txtRate control’s TextChanged event procedure. Type **Call ClearLabels()** and press **Enter**.

- 3. Save the solution, then start the application. Type **41** in the Hours box and then type **9** in the Rate box. Click the **Calculate** button. The regular pay, overtime pay, and gross pay amounts shown earlier in Figure 17-4 appear in the interface.

- 4. Now change the number of hours from 41 to 4. Changing the number of hours causes the txtHours control’s TextChanged event to occur. As a result, the computer processes the Call ClearLabels() statement entered in the event procedure. When processing the statement, the computer temporarily leaves the event procedure to process the code in the ClearLabels procedure. The assignment statements in the ClearLabels procedure remove the contents of three label controls in the interface. After processing the assignment statements, the computer processes the ClearLabels procedure’s End Sub clause, which ends the procedure. The computer then returns to the txtHours control’s TextChanged event procedure and processes the line of code located below the Call statement. In this case, the line below the Call statement is End Sub, which ends the event procedure.

- 5. Click the **Calculate** button, then change the rate of pay from 9 to **9.55**. Notice that the pay amounts are removed from the interface when you make a change to the rate. Click the **Calculate** button, then click the **Exit** button.

To complete the Weekly Pay application, you need to code the Clear button's Click event procedure. The procedure should remove the contents of both text boxes. It also should remove the pay amounts from the three label controls.

### To code the Clear button's Click event procedure, then test the procedure:

- 1. Open the code template for the btnClear control's Click event procedure. Type **'clear text boxes and label controls** and press **Enter** twice.
- 2. Type **txtHours.Text = String.Empty** and press **Enter**, then type **txtRate.Text = String.Empty** and press **Enter**. You can use the ClearLabels procedure to remove the pay amounts from the label controls. Type **Call ClearLabels()** and press **Enter**.
- 3. Save the solution, then start the application. Type **10** in the Hours box and then type **5** in the Rate box. Click the **Calculate** button. The values 50.00, 0.00, and 50.00 appear in the label controls. Click the **Clear** button to remove the contents of the text boxes and label controls, then click the **Exit** button.
- 4. Close the Code Editor window, then close the solution.

## MINI-QUIZ 1

- 1. The items in the Call statement are referred to as ________.
  - a. arguments
  - b. parameters
  - c. passers
  - d. None of the above.
- 2. You can enter your sub procedures ________ in the Code Editor window.
  - a. above the Public Class line
  - b. above the first event procedure
  - c. below the End Class line
  - d. All of the above.
- 3. When the contents of a text box changes, the text box's ________ event occurs.
  - a. ChangedText
  - b. ModifiedText
  - c. TextModified
  - d. TextChanged

procedure. When only the contents are passed, the receiving procedure is not given access to the variable in memory; therefore, it cannot change the value stored inside the variable. You pass a variable by value when the receiving procedure needs to know the variable’s contents, but the receiving procedure does not need to change the contents. Unless specified otherwise, variables are passed by value in Visual Basic. The Happy Birthday application, which you code in the next set of steps, passes two variables by value to a sub procedure.

### To open the Happy Birthday application, and then code the application:

- 1. Open the **Birthday Solution (Birthday Solution.sln)** file, which is contained in the ClearlyVB\Chap17\Birthday Solution folder. If necessary, open the designer window. When the user clicks the Display Message button, the button’s Click event procedure will prompt the user to enter a first name and age. It then will call a sub procedure to display the two input items in a birthday message, like this one: “Happy 18th Birthday, Rob!”

- 2. Open the Code Editor window. Locate the btnDisplay control’s Click event procedure. The code prompts the user to enter the first name and age (in years), and it stores the values in the strName and strAge variables.

- 3. You will use a sub procedure named DisplayMessage to display the birthday message. The sub procedure will need to know the person’s name and age, but it will not need to change either of those values. Therefore, you will pass the strName and strAge variables by value. First, enter the appropriate Call statement. Click the **blank line** above the End Sub clause in the btnDisplay control’s Click event procedure, then type **Call DisplayMessage(strName, strAge)** and press **Enter**. Don’t be concerned about the jagged line that appears below DisplayMessage in the Call statement. The jagged line will disappear when you enter the DisplayMessage procedure in the Code Editor window.

- 4. Now enter the DisplayMessage procedure. The procedure will need two parameters to store the values passed to it by the Call statement. Because the Call statement passes two strings, both parameters must be String variables. Click the **blank line** below the Public Class frmMain line, then press **Enter** to insert another blank line. Type **Private Sub DisplayMessage(ByVal strPerson As String, ByVal strYears As String)** and press **Enter**. See Figure 17-6. Notice that the number, data type, and sequence of the arguments in the Call statement match the number, data type, and sequence of the corresponding parameters in the procedure header. Also notice that the names of the parameters do not need to be identical to the names of the corresponding arguments. In fact, to avoid confusion, it usually is better to use different names for the arguments and parameters.
