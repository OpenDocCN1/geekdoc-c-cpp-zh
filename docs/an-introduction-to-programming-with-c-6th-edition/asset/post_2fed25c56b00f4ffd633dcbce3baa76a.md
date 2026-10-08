
# IPO chart information

# C++ instructions

## Input
department code (1, 2, or 3)

```
int deptCode = 0;
```

## Processing
none

## Output
salary
```
int salary = 0;
```

## Algorithm

- 1. enter the department code
2. if (the department code is one of the following):
   1 salary = 25000
   2 salary = 30000
   3 salary = 32000
   other display "invalid code"
   salary = 0
end if
3. display salary

Figure 6-42

12. Complete Try THIS Exercise 

10. Enter (or copy) the instructions from the Try12.cpp file into a new source file named ModifyTry12.cpp. Be sure to change the filename in the first comment. Modify the code in the ModifyTry12.cpp file so that it verifies the pay code is 1 through 10. If the code is not 1 through 10, prompt the user for the current pay. Instead, display the "Invalid pay" message. Save and run the program. Test the program using 1 and 500 as the pay code and current pay. Now test it using the following set of input values: 4 and 450, 9 and 500, 2 and 625, and 100, 600, and 160.

13. Kartlon wants a program that displays the amount of money a company owes for. The fee per person is based on the number of people the company registers, as shown in Figure 6-43. For example, if the company registers seven, then the total amount owed $560. If the user enters a number that is less than equal to zero, the program should display an appropriate error message.

| Number of registrants | Fee per person |
| :--- | :--- |
| 1 through 10 | $100 |
| 5 through 10 | $80 |
| 11 or more | $60 |

Figure 6-43

- Create an IPO chart for the problem, and desk-check the algorithm five times, using the 4, 8, 12, 0, and -2 as the number of people registered.

# CHAPTER 6 More on the Selection Structure

- b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier in Figure 6-42. Then code the algorithm into a program.

- c. Desk-check the program using the same data used to desk-check the algorithm.

- d. Enter your C++ instructions into a source file named Introductory13.cpp. Also enter appropriate comments and any additional instructions required by the compiler.

- e. Save and run the program. Test the program using the same data used to desk-check the program.

# INTERMEDIATE

- 14. The owner of Harry's Car Sales pays each salesperson a commission based on or her monthly sales. The sales ranges and corresponding rates are shown in Figure 6-44.

| Monthly sales ($) | Commission rate |
| :--- | :--- |
| 0 – 19,999.99 | 4% |
| 20,000 – 29,999.99 | 5% |
| 30,000 – 39,999.99 | 6% |
| 40,000 – 49,999.99 | 7% |
| 50,000 or more | 9% |
| Less than 0 | 0% |

Figure 6-44

- a. Create an IPO chart for the problem, and then desk-check the algorithm six times, using sales of 2500, 28500.35, 35678.99, 42300, 50000, and -3.

- b. List the input, processing, and output items, in a chart similar to the one shown earlier in Figure 6-42. Then code the algorithm into a program.

- c. Desk-check the program using the same data used to desk-check the algorithm.

- d. Enter your C++ instructions into a source file named Introductory14.cpp. Also enter appropriate comments and any additional instructions required by the compiler. Display the commission in fixed-point notation with two decimal places.

- e. Save and run the program. Test the program using the same data used to desk-check the program.

# INTERMEDIATE

- 15. In this exercise, you create a program that displays the number of daily calories needed to maintain your current weight. The number of calories is based on your gender, activity level, and weight. The formulas for calculating the daily calories are shown in Figure 6-45.

# Formulas

Moderately active female: total daily calories = weight multiplied by 12 calories per pound

Relatively inactive female: total daily calories = weight multiplied by 10 calories per pound

Moderately active male: total daily calories = weight multiplied by 15 calories per pound

Relatively inactive male: total daily calories = weight multiplied by 13 calories per pound

# Test data

| Gender | Activity | Weight |
| :--- | :--- | :--- |
| F | I | 150 |
| F | A | 120 |
| M | I | 180 |
| M | A | 200 |

Figure 6-45

- a. Create an IPO chart for the problem, and then desk-check the algorithm four times, using the test data in Figure 6-45.

- b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier in Figure 6-42. Then desk-check the program.

- c. Desk-check the program using the same data to desk-check the algorithm.

- d. Enter your C++ instructions into a source file named Intermediate15.cpp. Also enter appropriate comments and any additional instructions required by the compiler.

- e. Save and run the program. Test the program using the same data to desk-check the program.

16. In this exercise, you create a program that adds, subtracts, multiplies, or divides two integers. The program will need to get a letter (A for addition, S for subtraction, M for multiplication, or D for division) and two integers. If the user enters an invalid letter, the program should display an error message. If the letter is A (or a), the program should calculate and display the sum of both integers. If the letter is S (or s), the program should display the difference between both integers. When calculating the difference, always subtract the smaller number from the larger one. If the letter is M (or m), the program should display the product of both integers. If the letter is D (or d), the program should divide both integers, always dividing the larger number by the smaller one. Figure 6-46 shows the test data you will use for this exercise.

img/d6428a68f49d613bf2f170ac40ad_225.png

# CHAPTER 6 More on the Selection Structure

| Operation | First integer | Second integer |
| :--- | :--- | :--- |
| A | 10 | 20 |
| S | 45 | 15 |
| S | 65 | 50 |
| M | 7 | 13 |
| M | 10 | 20 |
| D | 45 | 15 |
| D | 50 | 100 |

Figure 6-46

- a. Create an IPO chart for the problem, and desk-check the algorithm using the test data shown in Figure 6-46.

- b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier in Figure 6-42. Then code the algorithm into a program.

- c. Desk-check the program using the same data to desk-check the algorithm.

- d. Enter your C++ instructions into a source file named Intermediate6.cpp. Also enter appropriate comments and any additional instructions required by the compiler.

- e. Save and run the program. Test the program using the same data to desk-check the program.

17. In this exercise, create a program that converts US Dollars to a different currency. The currencies and exchange rates are listed in Figure 6-47. The user should be allowed to choose the currency. (Hint: Design a code for each currency and use cout statements to display the code and corresponding currency.) The number of American Dollars should be an integer that is greater or equal to zero.

| Currency | Exchange rate |
| :--- | :--- |
| Canada Dollar | 1.01615 |
| Eurozone Euro | .638490 |
| Indian Rupee | 40.1798 |
| Japan Yen | 104.290 |
| Mexico Peso | 10.4613 |
| South Africa Rand | 7.60310 |
| United Kingdom Pound | .504285 |

Figure 6-47

- a. Create an IPO chart for the problem, and desk-check the algorithm nine times. For the first seven desk-checks, convert 10 American Dollars to each of the seven different currencies. For the eighth desk-check, test the algorithm using -3 as the number of American Dollars. For the last desk-check, test the algorithm using an invalid currency code.

- b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier in Figure 6-42. Then code the algorithm into a program.

c. Desk-check the program using the same data to desk-check the algorithm.

- d. Enter your C++ instructions into a source file named Advanced17.cpp. Also enter appropriate comments and any additional instructions required by the compiler. Display the results in fixed-point notation with two decimal places.

- e. Save and run the program. Test the program using the same data to desk-check the program.

18. Shopper Haven wants a program that displays the reward of points a customer earns each month. The reward points are based on the customer's membership type and total monthly purchase amount, as shown in Figure 6-48.

| Membership type | Total monthly purchase ($) | Reward points |
| :--- | :--- | :--- |
| Standard | Less than 75, 75–149.99, 150 and over | 5% of the total purchase, 7.5% of the total purchase, 10% of the monthly purchase |
| Plus | Less than 150, 150 and over | 6% of the total purchase, 13% of the monthly purchase |
| Premium | Less than 200, 200 and over | 4% of the total purchase, 15% of the monthly purchase |

Figure 6-48

a. Create an IPO chart for the problem, and desk-check the algorithm appropriately.

b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier in Figure 6-42. Then code the algorithm into a program.

c. Desk-check the program using the same data to desk-check the algorithm.

- d. Enter your C++ instructions into a source file named Advanced18.cpp. Also enter appropriate comments and any additional instructions required by the compiler. Display the reward points in fixed-point notation with no decimal places.

- e. Save and run the program. Test the program using the same data to desk-check the program.

19. In this exercise, you experiment with the switch statement.

a. Follow the instructions for starting C++ and opening the Advanced19.cpp file. The file is contained in either the C6\Chap6\Advanced19 Project folder or the C6\Chap6 folder. Run the program. When you are prompted to enter a grade, press Enter. If anything, did the switch statement display on the screen? Stop the program.
