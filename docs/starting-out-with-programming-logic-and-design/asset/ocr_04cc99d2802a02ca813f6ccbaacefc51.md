# Debugging Exercises 223

+   4. Design a loop that asks the user to enter a number. The loop should iterate 10 times and keep a running total of the numbers entered.

+   5. Design a For loop that calculates the total of the following series of numbers:
$$\frac{1}{30} + \frac{2}{29} + \frac{3}{28} + \dots + \frac{30}{1}$$

+   6. Design a nested loop that displays 10 rows of # characters. There should be 15 # characters in each row.

+   7. Convert the While loop in the following code to a Do–While loop:
Declare Integer x = 1
While x > 0
    Display "Enter a number."
    Input x
End While

+   8. Convert the Do-While loop in the following code to a While loop:
Declare String sure
Do
    Display "Are you sure you want to quit?"
    Input sure
While sure != "Y" AND sure != "y"

+   9. Convert the While loop to a For loop:
Declare Integer count = 0
While count < 50
    Display "The count is , count"
    Set count = count + 1
End While

+   10. Convert the For loop to a While loop:
Declare Integer count
For count = 1 To 50
    Display count
End For

# Debugging Exercises

+   1. Find the error in the following pseudocode:
Declare Boolean finished = False
Declare Integer value, cube
While NOT finished
    Display "Enter a value to be cubed."
    Input value;
    Set cube = value^3
    Display value, " cubed is \ cube
End While

+   2. The programmer intended the following pseudocode to display the numbers 1 through 60, and then display the message "Time’s up!" It will not function as intended, however. Find the error.
Declare Integer counter = 1
Const Integer TIME_LIMIT = 60