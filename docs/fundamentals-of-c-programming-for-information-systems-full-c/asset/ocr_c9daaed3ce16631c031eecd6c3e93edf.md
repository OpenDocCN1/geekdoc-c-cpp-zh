# CauseValidation Property

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

# Other Relevant Events

A variety of events are raised when you move from one control to another. These include

+   1. Enter
+   2. GotFocus
+   3. Leave
+   4. Validating
+   5. Validated
+   6. LostFocus

The complete code for computing grade in GradeWithImmediateValidation form is shown in Figure 3-19.