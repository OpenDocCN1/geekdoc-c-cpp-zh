# Program 15-1

```
1 Module calcButton_Click()
// Declare local variables to hold the test
// scores and the average.
Declare Real test1, test2, test3, average
// Get the first test score.
Set test1 = stringToReal(test1TextBox.Text)
// Get the second test score.
Set test2 = stringToReal(test2TextBox.Text)
// Get the third test score.
Set test3 = stringToReal(test3TextBox.Text)
// Calculate the average test score.
Set average = (test1 + test2 + test3) / 3
// Display the average test score in the
// averageLabel component.
Set averageLabel.Text = realToString(average)
```

```
23 Module exitButton_Click()
25 End Module
```

Here is a description of statement in the calcButton_click module:

+   * Line 4 declares local variables to hold the three test scores and the average of the test scores.
* Line 7 gets the value that has been entered into the testTextBox component, converts it to a real number, and stores it in the test1 variable.
* Line 10 gets the value that has been entered into the test2TextBox component, converts it to a real number, and stores it in the test2 variable.
* Line 13 gets the value that has been entered into the testTextBox component, converts it to a real number, and stores it in the test3 variable.
* Line 16 calculates the average of the three test scores and stores the result in the average variable.
* Line 20 converts the value in the average variable to a string and stores it in the averageLabel component's text property. Doing this displays the value in the label component.

The exitButton_click module executes the Close statement to close the window and subsequently end the program.

Figure 15-14 shows an example of how the program's window will appear after the user has entered values into the text boxes and clicked the calcButton component.