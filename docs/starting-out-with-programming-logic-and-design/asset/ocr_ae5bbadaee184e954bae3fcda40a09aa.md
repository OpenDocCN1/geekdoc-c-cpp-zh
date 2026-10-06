# 11.2 Modularizing a Menu-Driven Program 443

```
// Perform the selected operation.
Select menuSelection
Case 1:
    Call inchesToCentimeters()

Case 2:
    Call feetToCentimeters()

Case 3:
    Call milesToKilometers()
End Select
End Module
// The displayMenu module displays the menu and
// prompts the user for a selection. The selected
// value is validated and stored in the selection
// parameter, which is passed by reference.
// displayMenu(Integer ref selection)
Display the menu.
Display "1. Convert inches to centimeters."
Display "2. Convert feet to meters."
Display "3. Convert miles to kilometers."
Display

// Prompt the user for a selection.
Display "Enter your selection."
Input selection

// Validate the menu selection.
While selection < 1 OR selection > 3
    Display "That is an invalid selection."
    Display "Enter 1, 2, or 3."
    Input selection
End While
// The inchesToCentimeters module converts a
// measurement from inches to centimeters.
Module inchesToCentimeters()
// Local variables
Declare Real inches, centimeters

// Get the number of inches.
Display "Enter the number of inches."
Input inches

// Convert the inches to centimeters.
Set centimeters = inches * 2.54

// Display the result.
Display "That is equal to ", centimeters,
    " centimeters."
End Module
```