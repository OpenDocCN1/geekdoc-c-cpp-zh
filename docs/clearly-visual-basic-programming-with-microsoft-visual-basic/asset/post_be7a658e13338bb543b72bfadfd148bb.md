
5. How can you prevent the user from editing the contents of a text box while an application is running?

- a. Set the text box’s Editable property to False.
- b. Set the text box’s Changeable property to False.
- c. Set the text box’s ReadOnly property to True.
- d. Set the text box’s WriteOnly property to False.

## EXERCISES

- 1. In this exercise, you modify the Clock application coded in the chapter. Use Windows to make a copy of the Clock Solution folder. Save the copy in the ClearlyVB\Chap16 folder. Rename the copy Clock Solution-TRY THIS 1. Open the Clock Solution (Clock Solution.sln) file, which is contained in the ClearlyVB\Chap16\Clock Solution-TRY THIS 1 folder. Open the designer window, then open the Code Editor window. Modify the btnStart control’s Click event procedure so that it uses Do...Loop statements rather than For...Next statements. Use the Until keyword in the Do clause. Save the solution, then start and test the application. Stop the application, then close the solution. (The answers to TRY THIS Exercises are located at the end of the chapter.)

- 2. In this exercise, you modify the Clock application coded in the chapter. Use Windows to make a copy of the Clock Solution folder. Save the copy in the ClearlyVB\Chap16 folder. Rename the copy Clock Solution-TRY THIS 2. Open the Clock Solution (Clock Solution.sln) file, which is contained in the ClearlyVB\Chap16\Clock Solution-TRY THIS 2 folder. Open the designer window, then open the Code Editor window. Modify the btnStart control’s Click event procedure so that it uses a posttest loop to display the number of minutes. Use the While keyword in the Loop clause. Save the solution, then start and test the application. Stop the application, then close the solution. (The answers to TRY THIS Exercises are located at the end of the chapter.)

- 3. In this exercise, you modify one of the Monthly Payment Calculator applications coded in the chapter. Use Windows to make a copy of the Monthly Payment Solution-Version 1 folder. Save the copy in the ClearlyVB\Chap16 folder. Rename the copy Monthly Payment Solution-Version 1-MODIFY THIS. Open the Monthly Payment Solution (Monthly Payment Solution.sln) file contained in the Monthly Payment Solution-Version 1-MODIFY THIS folder. Open the designer window, then open the Code Editor window. Locate the btnCalc control’s Click event procedure. Currently, the procedure displays the payments by rate within term. Change the procedure’s code so it displays the payments by term within rate. Save the solution. Start and then test the application. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_380_0.png)

![](img/cf88270932e011575089da06b940a1d9_380_1.png)

![](img/cf88270932e011575089da06b940a1d9_380_2.png)

### INTRODUCTORY

- 4. In this exercise, you code an application that displays a bar chart. The bar chart depicts the ratings for five hotels. Open the Hotel Solution (Hotel Solution.sln) file, which is contained in the ClearlyVB\Chap16\Hotel Solution folder. The Create Bar Chart button's Click event procedure should allow the user to enter the hotel rating for each of five hotels. The rating can be from 1 through 6 only. Use the InputBox function to get each rating. If the user enters an invalid rating, the procedure should display an appropriate message in a message box, and then ask the user for the hotel's rating again. In other words, the procedure should not accept an invalid rating. Use each hotel's rating to display the appropriate number of asterisks in the bar chart. Figure 16-12 shows a sample run of the application after the user enters the following ratings: 4, 6, 3, 8, 6, and 2. Save the solution. Start and then test the application. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_381_0.png)

Figure 16-12: Sample run of the Hotel Ratings application

- 5. In this exercise, you modify one of the Monthly Payment Calculator applications coded in the chapter. Use Windows to make a copy of the Monthly Payment Solution-Version 2 folder. Save the copy in the ClearlyVB\Chap16 folder. Rename the copy Modified Monthly Payment Solution-Version 2. Open the Monthly Payment Solution (Monthly Payment Solution.sln) file contained in the Modified Monthly Payment Solution-Version 2 folder. Open the designer window, then open the Code Editor window. Locate the btnCalc control's Click event procedure. Change the procedure's code so it uses a Do...Loop statement to keep track of the terms. Save the solution. Start and then test the application. Stop the application, then close the solution.

### INTERMEDIATE

- 6. In this exercise, you modify the Clock application coded in the chapter. Use Windows to make a copy of the Clock Solution folder. Save the copy in the ClearlyVB\Chap16 folder. Rename the copy Modified Clock Solution. Open the Clock Solution (Clock Solution.sln) file contained in the Modified Clock Solution folder. Open the designer window. Currently, the interface and code display the number of hours and minutes. Modify the interface and code to also display the number of seconds. Use second values of 0 through 5 (rather than 0 through 59). Save the solution. Start and then test the application. Stop the application, then close the solution.

- 7. In this exercise, you code an application that displays a pattern of asterisks. Open the TwoToTenAsterisks Solution (TwoToTenAsterisks Solution.sln) file, which is contained in the ClearlyVB\Chap16\TwoToTenAsterisks Solution folder. The Display Asterisks button should display the pattern of asterisks shown below. The pattern contains 2 asterisks, 4 asterisks, 6 asterisks, 8 asterisks, and 10 asterisks. Display the pattern in the lblAsterisks control. Use a For...Next statement for the outer loop, and a Do...Loop statement for the nested loop. Save the solution, then start and test the application. Stop the application, then close the solution.

```
**
****
******
********
**********
```

### ADVANCED

- 8. In this exercise, you code an application for Cartwright Industries. Open the Cartwright Solution (Cartwright Solution.sln) file, which is contained in the ClearlyVB\Chap16\Cartwright Solution folder. The application should allow the user to enter the salesperson ID for any number of salespeople, as well as enter any number of sales amounts for a salesperson. Use the InputBox function to get the salesperson's ID and sales amounts. Total a salesperson's sales before moving on to the next salesperson. Display each salesperson's total sales, along with his or her ID, in the interface. When the user has finished entering data, display the company's total sales in the interface. Save the solution, then start and test the application. When you are finished testing the application, stop the application, then close the solution. Figure 16-13 shows a sample run of the application after the user enters the following IDs and sales amounts:

| ID | Sales amounts |
| --- | --- |
| AB2 | 300.35, 200.50, and 250.75 |
| BN4 | 45.67 and 350.05 |
| CR7 | 100.23, 67.45, and 35.85 |

![](img/cf88270932e011575089da06b940a1d9_383_0.png)

Figure 16-13: Sample run of the Cartwright Industries application

- 9. In this exercise, you create an application that displays a table consisting of three rows and seven columns. The first column should contain the numbers 1 through 3. The second and subsequent columns contain the result of multiplying the number in the first column by the numbers 0 through 5. Open the Table Solution (Table Solution.sln) file, which is contained in the ClearlyVB\Chap16\Table Solution folder. Code the Display Table button's Click event procedure. Save the solution, then click the Display Table button. Figure 16-14 shows a sample run of the application. Stop the application, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_383_1.png)

Figure 16-14: Sample run of the Table application
