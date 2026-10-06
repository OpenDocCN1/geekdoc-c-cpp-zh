# Chapter 8

# Arrays

start with 0 when counting people or things, so we used the expression index + 1 to start the employee numbers at 1.

# Processing the Elements of an Array

Processing array elements is no different than processing other variables. In our programs we show how you can assign values to array elements, store input in array elements, and display the contents of array elements. The following Inlight section shows how array elements can be used in math expressions.

# In the Spotlight:

# Using Array Elements in a Math Expression

Megans owns a small neighborhood coffee shop, and she has six employees who work as baristas (coffee bartenders). All of the employees have the same hourly pay rate. Megan has asked you to design a program that will allow her to enter the number of hours worked by each employee and display the amounts of all the employees' gross pay. You determine that the program should perform the following steps:

+   1. For each employee: get the number of hours worked and store it in an array element.
2. For each array element: use the value stored in the element to calculate employee's gross pay. Display the amount of the gross pay.

Program 8-4 shows the pseudocode for the program, and Figure 8-4 shows a flowchart.

# Program 8-4

```
// Constant for the size of the array.
Constant Integer SIZE = 6

// Array to hold each employee's hours.
Declare Real hours[SIZE]

// Variable to hold the hourly pay rate.
Declare Real payRate

// Variable to hold a gross pay amount.
Declare Real grossPay

// Variable to use as a loop counter.
Declare Integer index

// Get each employee's hours worked.
For index = 0 TO SIZE
    Display "Enter the hours worked by"
    Display "employee ", index + 1, "."
    Input hours[index]
End For

// Get the hourly pay rate.
Display "Enter the hourly pay rate."
Input payRate
```