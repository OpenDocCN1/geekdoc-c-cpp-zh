# Exercises

# Exercise 3-1

Create a new form named Exercise 3.1 within the project Ch3_DecisionAndValidation. Copy the controls and the code from the form IceCreamTotalDiscounted to the new form Exercise_3.1. Modify the form as shown below, so that it computes discount percent based on the discount code, not based on the subtotal: 20% discount if discount code is "1" and 10% discount if discount code is "2;" otherwise, there is no discount (if there is no discount, the user wouldn’t enter any discount code). The discount code is to be entered into a TextBox as shown below. Compute the discount using an if statement and also using a switch statement.

When the user clicks the compute button, the program should validate the data entered into the TextBoxes. The unit price must be a valid number; the number of scoops must be an integer; and if the user enters a discount code, it must be a "1" or "2."

Hint: To check whether a number is an integer, you may compare the number to the truncated number, as in

```
if (scoops == (int)scoops)
or,
if (scoops == Math.Truncate(scoops))
```

![](bbox=[0.1, 0.45, 0.7, 0.65])

# Exercise 3-2

Create a new form named Exercise 3.2 within the project Ch3_DecisionAndValidation. Copy the controls and code from the form IceCreamTotalDiscounted to the new form Exercise_3.2. Modify the form so that the user won’t be able to move away from the TextBox for scoops, if the data entered into the TextBox is not an integer. Display a message using the Error Provider. Highlight the data so that the user can type over it.

Hint: To check whether a number is an integer, you may compare the number to the truncated number, as in

```
if (scoops == (int)scoops)
or,
if (scoops == Math.Truncate(scoops))
```