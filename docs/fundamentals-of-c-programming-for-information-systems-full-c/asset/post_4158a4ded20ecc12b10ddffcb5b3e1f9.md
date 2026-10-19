
## Tutorial 3: switch Statement

To help understand the switch statement, you will create a form that computes the discount for a hotel room reservation based on the discount type ("AAA," "Best Rate," "Government" or "Senior"), as shown in Figure 3-7:

Figure 3-7: Reservation discount calculator

![](img/143bad48262566137acc9c41f668a88f_119_0.png)

Step 3-1: Open the project Ch_DecisionAndValidation.

Step 3-2: Open the form Reservation.

Step 3-3: Add the following code to the click event of btnComputeDiscount button.

```
private void btnComputeDiscount_Click(object sender, EventArgs e)
{
    string discountType = txtdiscountType.Text;
    float discountPercent;

    // Compute discount percent
    switch (discountType)
    {
        case "AAA":
            discountPercent = 10;
            break;
        case "Best Rate":
            discountPercent = 5;
            break;
        case "Government":
            discountPercent = 15;
            break;
        case "Senior":
            discountPercent = 12.5F;
            break;
        default:
            discountPercent = 0;
            break;
    }
    // Display discount percent
    lblDiscountPercent.Text = discountPercent.ToString("N");
```

Step 4-3: Add the following code to the beginning of btnGrade click event handler to get the score and validate it:

```
float totalScore;
// Verify that the score is a number
if (float.TryParse(txtScore.Text, out totalScore) == false)
{
    // Display invalid number message
    MessageBox.Show("Please enter a valid number for score");
    txtScore.Focus();
    txtScore.SelectAll();
    return;
}

// Get attendance
float attendance = float.Parse(txtAttendance.Text);
```

Step 4-4: Run the form and test it using valid and invalid score (non-numeric score and no score).

Figure 3-11 shows the complete code for GradeWithLateValidation form.

### Figure 3-11: Code for GradeWithLateValidation form

```
20  private void btnGrade_Click(object sender, EventArgs e)
21  {
22      float totalScore;
23      // Verify that the score is a number
24      if (float.TryParse(txtScore.Text, out totalScore) == false)
25      {
26          // Display invalid number message
27          MessageBox.Show("Please enter a valid number for score");
28          txtScore.Focus();
29          txtScore.SelectAll();
30          return;
31      }
32
33      // Get attendance
34      float attendance = float.Parse(txtAttendance.Text);
35
36      // Compute grade:
37      string letterGrade;
38      if (totalScore >= 90)
39          if (attendance >= 90F)
40              letterGrade = "A";
41          else
42              letterGrade = "B";
43      else if (totalScore >= 80)
44          letterGrade = "B";
45      else if (totalScore >= 70)
46          letterGrade = "C";
47      else
48          letterGrade = "F";
49
50      // Display grade:
51      lblGrade.Text = letterGrade;
52  }
```

An alternative to using a MessageBox to alert users of data errors is to use an **ErrorProvider** control.

### ErrorProvider Control

The ErrorProvider indicates an error by placing an error indicator image next to the control. Moving the mouse over the image displays the error message as a tooltip, as shown in Figure 3-15.

Figure 3-15: ErrorProvider control with error message

![](img/143bad48262566137acc9c41f668a88f_128_0.png)

Unlike the MessageBox, ErrorProvider can be used to indicate errors on multiple TextBoxes simultaneously.

To use an ErrorProvider, add the ErrorProvider control from the Container group in the Toolbox. To indicate error next to a control, use the SetError method of the ErrorProvider object, which specifies the control and the error message, as in

```
.SetError(controlName, errorMessage);
```

See the code in Figure 3-16 for an example. To remove the image, set the error message to a null string.

### Step 5-3: Drag and drop the ErrorProvider control from the Toolbox to the form. The ErrorProvider appears in the component tray at the bottom of the Designer window.

Change the name of the control from ErrorProvider1 to erpAttendance.

- Create the Validating event handler for txtAttendance.
- Add the code from lines 60–71 in Figure 3-16 to the Validating event handler of txtAttendance on the line following the opening brace "{".
- Run the form, enter an invalid data for attendance and try moving away by tabbing or clicking in the first TextBox.
- Repeat with valid data.

### Figure 3-16: Validating event handler with ErrorProvider

```
57
58 private void txtAttendance_Validating(object sender, CancelEventArgs e)
59 {
60     float attendance;
61     // Verify that attendance is a number
62     if (float.TryParse(txtAttendance.Text, out attendance) == false)
63     {
64         // Display invalid number message
65         errAttendance.SetError(txtAttendance, "Please enter a valid number for attendance");
66         txtAttendance.Focus();
67         txtAttendance.SelectAll();
68         return;
69     }
70     else
71         errAttendance.SetError(txtAttendance, "");
72 }
```

### Checking for Null Values

The code in the validation event of each TextBox would validate the data entered into it, if and only if the user tries to move away from the TextBox. What if the user skips a TextBox and clicks the button to compute grade? That may result in an undesirable abnormal termination of the program.

So, even with the validation codes we have, it is necessary to verify that the TextBoxes are not empty. This can be done in the click event handler of the btnGrade button, as shown in Figure 3-17.

Step 5-4: Add the if statement shown in Figure 3-17 to the beginning of btnGrade_click event handler.

Step 5-5: Run the form, and test the code when attendance data is missing and when invalid attendance data is entered.

### Figure 3-17: Checking for nulls in TextBoxes

```
private void btnGrade_Click(object sender, EventArgs e)
{
    // Verify that the TextBoxes are not empty
    if ((txtScore.Text.Length == 0) || (txtAttendance.Text.Length == 0))
    {
        MessageBox.Show("Please enter score and attendance");
        return;
    }

    // Get totalScore and attendance
    ...
```

### CauseValidation Property

When you move focus from one control to another, the Validating event for the first control is raised only if the CauseValidation property of both controls are true, which is the default.

Step 5-6: Set CauseValidation for txtAttendance to False. Run the form, enter an invalid score into txtScore and press the Tab key. No message is displayed, indicating that the Validating event for txtScore was not raised.

You can use the CauseValidation property to allow users to move away from a control without entering valid data. For example, you can let the user close the form without entering valid data by clicking the Exit button. To suppress the Validating event when the user moves to the Exit button, set the CauseValidation property of the Exit button to false.

Step 5-7: Add a new button, btnExit, and set its CauseValidation property to false. Enter the code shown in Figure 3-18 to the click event handler of btnExit. Run the form. Enter an invalid score and click the Exit button. No error message is displayed because setting CauseValidation of Exit button to false suppresses the validating event of the TextBox.

Figure 3-18: Click event handler of Exit button

```
private void btnExit_Click(object sender, EventArgs e)
{
    Environment.Exit(0); // 0 is an exit code passed to the O.S.
    // Environment.Exit closes all "threads"; but this.Close doesn't
}
```

### Other Relevant Events

A variety of events are raised when you move from one control to another. These include

- 1. Enter
- 2. GotFocus
- 3. Leave
- 4. Validating
- 5. Validated
- 6. LostFocus

The complete code for computing grade in GradeWithImmediateValidation form is shown in Figure 3-19.
