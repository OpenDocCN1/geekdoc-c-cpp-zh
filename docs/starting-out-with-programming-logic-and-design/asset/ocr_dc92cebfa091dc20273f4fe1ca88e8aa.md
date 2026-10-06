# 15.3 Writing Handlers

When this program runs, there are two possible events that we want to respond to: the user clicking the calcButton component and the user clicking the exitButton component. If the user clicks the calcButton component, we want the program to calculate the gross pay and display it in the grossLabel component. If the user clicks the exitButton component, we want the program to end.

To handle the event that occurs when the user clicks the calcButton, we would write the following event handler in pseudocode:

```
Module calcButtonClick(
  // Local variables to hold the hours worked,
  // pay rate, and the gross pay.
  Declare Real hours, payRate, grossPay
  // Get the number of hours worked from the
  // textBox component.
  Set hours = stringToReal(textBox.Text)
  // Get the pay rate from the payTextBox
  Set payRate = stringToReal(payTextBox.Text)
  // Calculate the gross pay.
  Set grossPay = hours * payRate
  // Display the gross pay in the grossLabel
  Set grossPayLabel.Text = realToString(grossPay)
End Module
```

Let's look at each statement in this event handler.

+   - Line 4 declares three variables: hours, payRate, and grossPay.
- Line 8 gets the value that has been typed into the textBox component and assigns it to the hours variable. A lot of things are happening in this line, so it deserves a thorough explanation.

When the user enters a value into a text box, the value is stored in the component's Text property. In pseudocode, we use dot notation to refer to a component's Text property. For example, to refer to the textBox component's Text property, we write textBox.Text.
In many languages, you cannot assign the value of a component's Text property directly to a numeric variable. For example, if line 8 were written as, an error would occur:

```
Set hours = textBox.Text
```

This logic will cause an error because the Text property holds strings, and strings cannot be assigned to numeric variables. So, we need to convert the value in the Text property to a real number. This can be done with the stringToReal function, as:

```
Set hours = stringToReal(textBox.Text)
```

(We discussed the stringToReal function in Chapter 6.)

+   - Line 12 gets the value that has been typed into the payTextBox component, converts it to a real number, and assigns it to the payRate.