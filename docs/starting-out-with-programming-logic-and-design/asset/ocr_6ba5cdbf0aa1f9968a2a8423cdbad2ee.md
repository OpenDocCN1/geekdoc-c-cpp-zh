# Chapter 11 Menu-Driven Programs

> NOTE: As a third alternative, the program could also be modified to use an If-Else If statement.

# Validating the Menu Selection

Any program that allows the user to select an item from a menu should validate the user's selection. Program 11-1 validated the user's menu selection with the Default section in the case structure (in lines 45 through 47). Program 11-2 validated the menu selection with the Else clause (in lines 43 through 45).

An alternative approach is to use an input validation loop immediately after the Input statement that reads the user's selection. If the menu selection is invalid, the loop displays an error message and prompts the user to enter again. The loop repeats as long as the input is invalid.

The pseudocode in Program 11-3 shows how Program 11-1 can be modified to use an input validation loop. The input validation loop appears in lines 25 through 25. Notice that the case structure does not have a Default section. The input validation loop makes sure the menuSelection variable is set to a value in the range of 1 through 3 before the program enters the case structure. Figure 11-4 shows a flowchart for the program.

# Program 11-3

```
1 // Declare a variable to hold the
2 // user's menu selection.
3 Declare Integer menuSelection
4
5 // Declare variables to hold the units
6 // of measurement.
7 // Declare inches, centimeters, feet, meters,
8 miles, kilometers
9
10 // Display the menu.
11 Display "1. Convert inches to centimeters."
12 Display "2. Convert feet to meters."
13 Display "3. Convert miles to kilometers."
14 Display
15
16 // Prompt the user for a selection
17 Display "Enter your selection."
18 Input menuSelection
```