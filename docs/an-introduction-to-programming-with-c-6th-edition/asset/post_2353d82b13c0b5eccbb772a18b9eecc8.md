
# CHAPTER 8 More on the Repetition Structure

| Line | numAsterisks |
|---|---|
| 1 | * \n ** \n *** \n **** |
| Output | ****

Figure-20 Desk-check table and output after the nested loop cout statement is processed the fourth time.

Here, the computer adds the number 1 to the value stored in the numAsterisks variable, giving 5. The computer then checks whether the variable's value is less than 6. It is, so the nested loop cout << '*'; statement displays another asterisk on the current line on the computer screen. Figure-21 shows the desk-check table and output after the cout statement is processed the fifth time.

| Line | numAsterisks |
|---|---|
| 1 | * \n ** \n *** \n **** \n ***** |
| Output | ***** |Figure-21 Desk-check table and output after the nested loop cout statement is processed the fifth time.

The value stored in the numAsterisks variable is updated once again; this time, the result is 6. The computer checks whether the variable's value is less than 6. It is not, so the nested loop ends and the numAsterisks variable is removed from the computer's internal memory. Continuing with the first statement following the end of the nested loop. In this case, the cout << endl; statement positions the cursor on the next line on the computer screen. The cout << endl; statement is the last statement in the body of the outer loop. Therefore, after processing the statement, the computer returns to the condition argument. This update (line += 1) tells the computer to add the number 1 to the value stored in the line; the result is 2. The condition (line < 4) directs the computer to check whether the variable's value is less than 4. It is, so the instructions in the body of the outer loop are processed again. The first instruction is the nested loop for clause, while initialization and condition arguments tell the computer to create the numAsterisks variable and initialize it to the number 1, and then check whether its value is less than 6. At this point, the variable's value is less than 6, so the cout << '*'; in the nested loop is processed. That statement displays an asterisk on the second line on the computer screen. Figure-22 shows the current status of the desk-check table and output.

> Recall from Chapter 7 that the variable created in the for clause is local to the for statement and is removed when the loop ends.

# The Asterisks Program

| line | numAsterisks |
| --- | --- |
| # | # |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |

Output
****

Figure-82 Current status updates the value in the numAsterisks variable by adding the number 1 to it; the result is 2. The computer then checks whether the variable's value is less than 6, so the nested loop's cout << '*'; statement another asterisk on the current line on the computer screen. The computer adds the number 1 to the value stored in the numAsterisks variable, giving 3. It then checks whether the variable's value is less than 6. It is, the cout << '*'; statement displays the third asterisk on the current line on the computer screen. Once again, the computer adds the number 1 to the value stored in the numAsterisks variable and checks whether the value is 4, so the cout << '*'; statement displays the fourth asterisk on the current line on the computer screen. The computer adds the number 1 to the value stored in the numAsterisks variable and checks whether the value (which is now 5) is less than 6. It is, so the cout << '*'; statement displays the fifth asterisk on the current line on the computer screen. Once again, the computer updates the value stored in the numAsterisks variable by adding the number 1 to it; the result is 6. The computer then checks whether the variable's value is less than 6. It's not, so the nested loop ends and the numAsterisks variable is removed from the computer's internal memory. Figure-23 shows the desk-check table and output after the nested loop ends the second time. Notice that the nested loop completely proceeded to the next iteration of the outer loop.

| line | numAsterisks |
| --- | --- |
| # | # |
| 2 | 2 |
| 3 | 3 |
| 4 | 4 |
| 5 | 5 |
| 6 | 6 |

Output
***

Figure-23 Desk-check table and output after the nested loop ends the second time.

# CHAPTER 8 More on the Repetition Structure

Processing continues with the first statement located below the nested loop—in this case, the cout << endl; statement positions the cursor on the next line on the computer screen. After processing the statement, the computer returns to the outer loop's for clause to process the update and condition arguments. The update line += 1 tells the computer to add the number 1 to the value stored in the line; the result is 3. The condition (line < 4) directs the computer to check whether the variable's value is less than 4. It is, so the instructions in the body of the outer loop are processed again. The first instruction is the nested loop for for clause, where initialization and condition arguments tell the computer to create the numAsterisks variable and initialize it to the number 1, and then check whether its value is less than 6. At this point, the variable's value is less than 6, so the cout << '*'; statement in the nested loop is processed. The computer displays the first asterisk on the next line on the computer screen. The computer will continue processing the nested loop until the value stored in the numAsterisks variable is the number 6. Figure-24 shows the desk-check and output after the nested loop ends the third time.

Processing continues with the cout << endl; statement, which follows the nested loop and the last statement in the body of the outer loop. That statement positions the cursor on the next line on the computer screen. After processing the statement, the computer returns to the outer loop's for clause to process its update and condition arguments. The update line += 1 tells the computer to add the number 1 to the value stored in the line; the result is 4. The condition (line < 4) directs the computer to check whether the variable's value is less than 4. It's not, so the outer loop ends and the line variable is removed from the memory. Processing will continue with the first statement located below the end of the outer loop. Figure 8-25 shows a sample run of the asterisks program.

# The Savings Calculator Program

The savings calculator program calculates the value of a one-time deposit into savings accounts that earns a specific amount of interest for a certain amount of time. The figure also includes sample calculations. The formula in Example 1 calculates the savings balance at the end of the first year. This does this by adding the number 1 to the interest rate of .03 and then raising the sum (1.03) to the first power. Recall that the result of raising a number to a power of 1 is the number itself; in this case the result is 1.03. The formula in Example 1 multiplies the number 1.03 by the number 1000, giving 1030. The formula in Example 2 calculates the account balance at the end of the third year. Here again, the formula begins by adding the number 1 to the interest rate of .03; however, it raises the sum (1.03) to the third power. Raising a number to the power of 3 multiplies itself three times; in this case the expression 1.03 * 1.03 * 1.03 yields 1.092727. The formula then multiplies the number 1.092727 by the number 1000, giving 1092.73 when rounded to two decimal places. Figure 8-26 shows the program's IPO chart and desk-check table. Note that the algorithm uses a counter to keep track of the years, which are from 1 to 5. It uses a postloop to calculate and display the account balance at the end of each year. The flowchart for this program is contained in the Ch8Charts.pdf file, which is located in the C6p(Chapter08) folder.

# Problem specification

For your 21st birthday, your grandmother opens an account for you and deposits $1000 into the account. The savings account pays a 3% interest on the account balance. If you don't deposit more money into the account, and you don't withdraw any money from it for 5 years, create a program that generates your answers would at the end of 1st year. You can calculate the answers using the following formula: b = p * (1 + r)^n, where p is the principal (amount of the deposit), r is the interest rate, n is the number of years, and b is the balance in the savings account at the end of the nth year.
