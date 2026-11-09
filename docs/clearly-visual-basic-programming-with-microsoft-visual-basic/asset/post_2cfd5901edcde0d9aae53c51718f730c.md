
| Test data | Expected result |
|---|---|
| No data entered | $0.00 |
| Valid values: | |
| 0 | $0.00 |
| 10 | $50.00 |
| 25 | $125.00 |
| 4.5 | $22.50 |
| -3 | ($15.00) |
| -6.5 | ($32.50) |
| Invalid values: | |
| x, #, 30 | $0.00 |

Figure 12-6: Testing chart for the Only Cookies-Version 1 application

The third guideline in Figure 12-1 pertains to selection structures. You can skip the third guideline because the application's code does not contain a selection structure. In this first set of steps, you will test the application using the test data and expected results listed in Figure 12-6.

### To test the Only Cookies-Version 1 application:

- 1. Start Visual Studio 2008 (or Visual Basic 2008 Express Edition). Open the **Only Cookies Solution** (**Only Cookies Solution.sln**) file, which is contained in the ClearlyVB\Chap12\Only Cookies Solution-Version 1 folder. If necessary, open the designer window.
- 2. Start the application. First, test the application without entering any data. Click the **Calculate** button. The expected result, $0.00, appears in the Total price box.
- 3. Type **0** in the Pounds ordered box, then click the **Calculate** button. The expected result, $0.00, appears in the Total price box. Change the number of pounds ordered to **10**, then click the **Calculate** button. $50.00 appears in the Total price box, which is correct.
- 4. On your own, test the application using the following valid values: **25, 4.5, -3, and -6.5**. The total prices should agree with the corresponding results listed in Figure 12-6.
- 5. Change the number of pounds ordered to **x**, then click the **Calculate** button. The TryParse method in the button's **Click** event procedure cannot convert the letter x to the Decimal data type, so it assigns the number 0 to the decOrdered variable. The decTotalPrice = decOrdered * intPRICE statement calculates the total price (0). The last assignment statement in the procedure formats the total price with a dollar sign and two decimal places, and then displays the result shown in the testing chart—$0.00.

![](img/cf88270932e011575089da06b940a1d9_273_0.png)

Figure 12-10: Result of entering a non-integer in the text box

- 6. Change the number of pounds ordered to **-6.5**, then click the **Calculate** button. $0.00 appears in the Total price box. Here again, the total price is misleading. Click the **Exit** button.

## STOP! THIS IS A RESTRICTED AREA!

The Only Cookies-Version 2 application expects the user to enter the number of pounds as an integer. The number of pounds should not contain any letters, periods, or special characters. Unfortunately, you can’t stop the user from trying to enter an inappropriate character into a text box. However, you can prevent the text box from accepting the character; you do this by coding the text box’s KeyPress event procedure. A control’s **KeyPress event** occurs each time the user presses a key while the control has the focus. When the KeyPress event occurs, a character corresponding to the pressed key is sent to the KeyPress event’s *e* parameter, which appears between the parentheses in the event’s procedure header. For example, when the user presses the period while entering data into a text box, the text box’s KeyPress event occurs and a period is sent to the event’s *e* parameter. Similarly, when the Shift key along with a letter is pressed, the uppercase version of the letter is sent to the *e* parameter. To prevent a text box from accepting an inappropriate character, you first use the *e* parameter’s **KeyChar property** to determine the pressed key. (KeyChar stands for “key character.”) You then use the *e* parameter’s **Handled property** to cancel the pressed key if it is an inappropriate one. Figure 12-11 shows examples of using the KeyChar and Handled properties in the KeyPress event procedure. Notice that you refer to the Backspace key on your keyboard using the **ControlChars.Back constant**. The Backspace key is necessary for editing the text box entry.

| Test data | Expected result |
|---|---|
| No data entered | $0.00 |
| **Valid values:** | |
| 0 | $0.00 |
| 10 | $50.00 |
| 25 | $125.00 |
| -3 | ($15.00) |
| **Invalid values:** | |
| x, #, O, 4.5, -6.5 | not allowed in the text box |

Figure 12-12: Testing chart for the modified Only Cookies-Version 2 application

### To modify the Only Cookies-Version 2 application, then test the application:

- 1. Open the Code Editor window. Open the code template for the txtOrdered control’s KeyPress event procedure. Enter the comments and five lines of code shown in Example 2 in Figure 12-11.
- 2. Start the application. On your own, test the application without entering any data, then test it using the following values: **0, 10, 25, and -3**.
- 3. Now test the application using the following values: **x, #, and O** (be sure to type the uppercase letter O rather than the number 0), **4.5, and -6.5**. You will not be able to enter the letter x, the # symbol, the uppercase letter O, or the period.
- 4. Click the **Exit** button. Close the Code Editor window, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_275_0.png)

For more examples of applications that require numeric data, see the Numeric Data Testing section in the Ch12WantMore.pdf file.

## MINI-QUIZ 1

- 1. What is the first guideline for selecting test data?
- 2. If the txtSales control contains the number 345.78, the Integer.TryParse(txtSales.Text, intSales) statement will assign __________ to the intSales variable.
- 3. When the user types the number 9 in a text box, the 9 is sent to the KeyPress event’s __________ parameter.

## THE SHADY HOLLOW HOTEL-VERSION 1 APPLICATION

The daily rate for a Standard room at Shady Hollow Hotel is $90. The daily rate for a Deluxe room is $115, and the daily rate for a Suite is $130. Figure 12-13 shows the interface for the Shady Hollow Hotel-Version 1 application. The interface uses radio buttons for the room type selection. When the user clicks the Display Rate button, its Click event procedure displays the daily rate in the interface. The Click event procedure is shown in Figure 12-14.

![](img/cf88270932e011575089da06b940a1d9_276_0.png)

**Figure 12-13:** Interface for the Shady Hollow Hotel-Version 1 application

```vb
Private Sub btnDisplay_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' displays a room's daily rate

    Dim intDailyRate As Integer

    Select Case True
        Case radStandard.Checked
            intDailyRate = 90
        Case radDeluxe.Checked
            intDailyRate = 115
        Case Else
            intDailyRate = 130
    End Select

    ' display daily rate
    lblDaily.Text = intDailyRate.ToString("C0")
End Sub
```

Test each path in this selection structure.

**Figure 12-14:** Display Rate button's Click event procedure in the Shady Hollow Hotel-Version 1 application

Before testing the Shady Hollow Hotel-Version 1 application, you will use the guidelines from Figure 12-1, as well as the interface and code shown in Figures 12-13 and 12-14, to create a set of test data. The first guideline is to test the application without entering any data. If no radio buttons are selected, the Daily rate box should show $0. The second guideline pertains to numbers entered in a text box; you can skip this guideline because the application does not use any text boxes. The third guideline covers selection structures. The application’s code contains one selection structure, which is located in the Display Rate button’s Click event procedure. According to the third guideline, you need to test each path in the selection structure. The first path’s condition (radStandard.Checked) will evaluate to True when the Standard room radio button is selected; when the condition is True, $90 should appear in the Daily rate box. The second path’s condition (radDeluxe.Checked) will evaluate to True when the Deluxe room radio button is selected; when this condition is True, $115 should appear in the Daily rate box. The third path, which is the Case Else path, is processed when the other two path conditions evaluate to False. When the Case Else path is processed, $130 should appear in the Daily rate box. Figure 12-15 shows the application’s testing chart.

| Test data | Expected result |
|---|---|
| No data entered | $0 |
| Standard room radio button selected | $90 |
| Deluxe room radio button selected | $115 |
| Suite radio button selected | $130 |

Figure 12-15: Testing chart for the Shady Hollow Hotel-Version 1 application

### To test the Shady Hollow Hotel-Version 1 application:

- 1. Open the **Shady Hollow Solution (Shady Hollow Solution.sln)** file, which is contained in the ClearlyVB\Chap12\Shady Hollow Solution-Version 1 folder. If necessary, open the designer window.
- 2. Start the application. First, test the application without entering any data. Click the **Display Rate** button. The Daily rate box shows $130, which is the daily rate for a Suite. The $130 rate is not correct, because the Suite radio button is not selected in the interface. Click the **Exit** button to end the application.
- 3. Open the Code Editor window. Locate the btnDisplay control’s Click event procedure. Notice that the Suite rate is assigned in the Case Else clause, which is processed when the Standard room and Deluxe room radio buttons are not selected. In other words, it’s processed when the Suite radio button is selected (which is correct) and also when no radio button is selected (which is incorrect). You can fix the problem by changing the Case Else clause to Case radSuite.Checked; doing this tells the computer to display $130 only when the Suite radio button is selected. You also can fix the problem by designating one of the radio buttons as the default radio button. Designating a default radio button ensures that a radio button is automatically selected when the interface first appears; it also is a common practice in Windows applications, as you learned in Chapter 11.
