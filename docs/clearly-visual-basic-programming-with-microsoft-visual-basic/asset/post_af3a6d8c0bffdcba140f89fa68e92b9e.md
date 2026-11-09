
- **Procedure-level variables**—variables declared in a procedure; have procedure scope
- **Scope**—the area where a variable is recognized in an application's code
- **String**—text enclosed in double quotation marks
- **ToString method**—a method used to convert the contents of a numeric variable to text; also formats the number
- **TryParse method**—used to convert text to a numeric data type
- **Variables**—memory locations whose contents can change while an application is running

## ANSWERS TO MINI-QUIZZES

### MINI-QUIZ 1

- 1. Integer
- 2. d. dblPay.Rate
- 3. Dim dblHoursWorked As Double

### MINI-QUIZ 2

- 1. Decimal.TryParse(txtIncome.Text, decIncome)
- 2. Const intMINIMUM As Integer = 55
- 3. lblSales.Text = decSales.ToString("C0")

## REVIEW QUESTIONS

- 1. Which of the following statements declares a variable named intNumSold?
  - a. Dim intNumSold As Integer
  - b. Dim As Integer intNumSold
  - c. Const intNumSold As Integer
  - d. None of the above.
- 2. If the user enters the text A34 in the txtPrice control, the TryParse(txtPrice.Text, decPrice) statement will assign __________ to the decPrice variable.
  - a. A
  - b. A34
  - c. 0
  - d. 34
- 3. Which of the following statements adds together the contents of the intScore1 and intScore2 variables, and then multiplies the sum by 2, assigning the result to the intTotal variable?
  - a. `intScore1 + intScore2 * 2 = intTotal`
  - b. `(intScore1 + intScore2) * 2 = intTotal`
  - c. `intTotal = intScore1 + intScore2 * 2`
  - d. None of the above.
- 4. Which of the following statements declares the decRATE named constant and initializes it to .15?
  - a. `Con decRATE As Decimal = .15`
  - b. `Const decRATE As Decimal = .15`
  - c. `Constant decRATE As Decimal = .15`
  - d. None of the above.
- 5. Which of the following statements formats the contents of the dblDue variable with a dollar sign and two decimal places?
  - a. `lblDue.Text = dblDue.ToString("C2")`
  - b. `lblDue.Text = dblDue.ToCurrency("C2")`
  - c. `lblDue.Text = ToString(dblDue, "C2")`
  - d. `lblDue.Text = dblDue.ToFormat("C2")`

## EXERCISES

### TRY THIS

- 1. In this exercise, you modify the Commission Calculator application from Chapter 6 so that it uses variables and the TryParse method. (The answers to TRY THIS Exercises are located at the end of the chapter.)
  - a. Open the Commission Calculator Solution (Commission Calculator Solution.sln) file contained in the ClearlyVB\Chap07\Commission Calculator Solution folder. Modify the code so that it uses variables and the TryParse method. Format the commission with a dollar sign and two decimal places.
  - b. Save the solution, then start and test the application. Stop the application, then close the solution.

### TRY THIS

- 2. In this exercise, you code an application that calculates and displays the amount of an employee’s new weekly pay. Figure 7-15 shows the output, input, and algorithm. (The answers to TRY THIS Exercises are located at the end of the chapter.)

```
Output:      new weekly pay
Processing:  weekly raise
Input:       current weekly pay
Algorithm:
1. enter the current weekly pay
2. calculate the weekly raise by multiplying the current weekly pay by .03
3. calculate the new weekly pay by adding the weekly raise to the current weekly pay
4. display the new weekly pay
```

Figure 7-15

- a. Open the New Pay Solution (New Pay Solution.sln) file contained in the ClearlyVB\Chap07\New Pay Solution folder. Code the algorithm using Decimal variables. Use a Decimal named constant for the raise rate of .03. Format the new weekly pay with a dollar sign and two decimal places.
- b. Save the solution. Desk-check the program using 200 and 330 as the current weekly pay.
- c. Start and then test the application. Stop the application, then close the solution.

### MODIFY THIS

- 3. In this exercise, you modify the Circle Area application created in the chapter.
  - a. Use Windows to make a copy of the Circle Area Solution folder. Save the copy in the ClearlyVB\Chap07 folder. Rename the copy Modified Circle Area Solution.
  - b. Open the Circle Area Solution (Circle Area Solution.sln) file contained in the Modified Circle Area Solution folder. Modify the code so that it uses a separate calculation for the radius squared. Assign the result of the radius squared calculation to a variable, then modify the area calculation appropriately.
  - c. Save the solution. Start the application, then test it using 4.6 as the radius. The area should be 66.48. Stop the application, then close the solution.

### INTRODUCTORY

- 4. The cashier at Jackson College wants an application that displays the total amount a student owes for the semester, including tuition and room and board. The tuition is $100 per semester hour, and room and board is $1800 per semester. The cashier will need to enter the number of hours the student is enrolled. Use Integer named constants for the semester hour fee and the room and board fee. Use Integer variables for the input and output items, as well as for any processing items you choose to use. Format the output with a dollar sign and no decimal places.
  - a. List the output and input items, as well as any processing items, then create an appropriate algorithm.
  - b. Create a new Visual Basic Windows application. Assign the name Jackson Project to the project. Assign the name Jackson Solution to the solution. Save the application in the ClearlyVB\Chap07 folder. Change the name of the form file on your disk to frmMain.vb. If necessary, change the form's name to frmMain.
  - c. Create an appropriate interface. Include an Exit button. Code the Exit button's Click event procedure and the problem's algorithm. Save the solution. Desk-check the program using your own sample data.
  - d. Start and then test the application. Stop the application, then close the solution.

### INTRODUCTORY

- 5. A concert hall has three seating categories: Orchestra, Main floor, and Balcony. Orchestra seats are $25. Main floor seats are $30, and Balcony seats are $15. The manager wants an application that allows him to enter the number of tickets sold in each seating category. The application should calculate the amount of revenue generated by each seating category, as well as the total revenue.
  - a. List the output and input items, as well as any processing items, then create an appropriate algorithm.
  - b. Create a new Visual Basic Windows application. Assign the name Concert Project to the project. Assign the name Concert Solution to the solution. Save the application in the ClearlyVB\Chap07 folder. Change the name of the form file on your disk to frmMain.vb. If necessary, change the form's name to frmMain.
  - c. Create an appropriate interface. Include an Exit button. Code the Exit button's Click event procedure and the problem's algorithm. Save the solution. Desk-check the program using your own sample data.
  - d. Start and then test the application. Stop the application, then close the solution.

### INTERMEDIATE

- 6. In this exercise, you modify the application you created in Exercise 5. In addition to calculating and displaying the revenue for each seating category, as well as the total revenue, the application should now display the percentage of the total revenue contributed by each seating category.
  - a. Use Windows to make a copy of the Concert Solution folder. Save the copy in the ClearlyVB\Chap07 folder. Rename the copy Modified Concert Solution.
  - b. Open the Concert Solution (Concert Solution.sln) file contained in the Modified Concert Solution folder. Make the appropriate modifications to the interface and code. Use Decimal variables to store the percentages. Display the percentages with a percent sign and one decimal place.
  - c. Save the solution, then start and test the application. Stop the application, then close the solution.

### INTERMEDIATE

- 7. In this exercise, you modify the Circle Area application created in the chapter. For this exercise, the circle will represent a pizza. In addition to displaying the area of the
