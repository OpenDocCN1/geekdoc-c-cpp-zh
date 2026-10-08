
# CHAPTER 10 Void Functions

to Intermediate17.cpp. Modify the program so that it uses void functions: one to determine the fat calories and the other to determine the fat percentage. Save and then run the program. Test the program appropriately.

## INTERMEDIATE

- 18. In this exercise, you create a simple payroll program using a main function and four void functions.
  - a. Figure 10-35 shows the IPO chart information for the payroll program. Complete the C++ instructions column for the main function, as well as for the void functions calcFedTaxes, calcNetPay, and displayInfo. The FWT (Federal Withholding Tax) rate is 20% of the weekly salary, and the FICA (Federal Insurance Contributions Act) rate is 8% of the weekly salary.
  - b. If necessary, create a new project named Intermediate18 Project. Enter your C++ instructions into a source file named Intermediate18.cpp. Also enter appropriate comments and any additional instructions required by the compiler. Display the taxes and net with two decimal places.
  - c. Save and then run the program. Test the program using 500 and 650 as the salary.

| main function IPO chart information | C++ instructions |
|---|---|
| salary | |
| FWT rate (2) | |
| FICA rate (.08) | |
| Processing | |
| none | |
| Output | |
| FWT | |
| FICA | |
| net pay | |

```
Algorithm
1. repeat while (the salary > 0)
2. call calcFedTaxes function to calculate the FWT and FICA, pass the function the salary, FWT rate, FICA rate, and the addresses of variables in which to store the FWT and FICA

call calcNetPay function to calculate the net pay, pass the salary, FWT, FICA, and the address of the variable in to store the net pay.
```

Figure 10-35 (continues)

(continued)

call the displayInfo function to display the FWT, FICA, and net pay, pass the function the FWT, FICA, and net pay

enter the salary
end repeat

### calcFedTaxes function
IPO chart information
Input
C++ instructions

- salary (formal parameter)
FWT rate (formal parameter)
FICA rate (formal parameter)
addresses of variables to store:
FWT (formal parameter)
FICA (formal parameter)

# Processing
none

# Output
FWT
FICA

# Algorithm

- 1. calculate the FWT by multiplying the salary by the FWT rate
2. calculate the FICA by multiplying the salary by the FICA rate

### calcNetPay function
IPO chart information
Input
C++ instructions

- salary (formal parameter)
FWT (formal parameter)
FICA (formal parameter)
address of a variable to store:
net pay (formal parameter)

# Processing
none

# Output
net pay

# Algorithm
calculate the net pay by subtracting the FWT and FICA from the salary

Figure 10-35 (continues)

(continued)

| displayInfo function | C++ instructions |
|---|---|
| Input | | FWT (formal parameter) FICA (formal parameter) net pay (formal parameter) |
| Processing | none |
| Output | | FWT FICA net pay |
| Algorithm | | display display the FWT, FICA, and net pay |

10-35

- 19. The payroll manager at Gerston Blankets wants a program that calculates and displays the gross pay for each of the company's employees. It should also calculate and display the total gross pay. The payroll manager will enter the number of hours the employee worked and receive time and one-half for the hours over 40. Employees working more than 40 hours use a function to determine an employee's gross pay. Use a value-returning function to accumulate the total gross pay. The program should display the total gross pay only after the payroll manager has finished the data for all employees. Use a sentinel value to end the program.
  - a. Create IPO charts for the problem, and desk-check the algorithm using the following four sets of hours worked and pay rates: 35, $10.50; $43, $15; $32, $9.75; $20, $6.45.
  - b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one showed earlier in Figure 10-35. Then, code the algorithm into a program.
  - c. Desk-check the program using the same data used to desk-check the algorithm.
  - d. If necessary, create a new project named Intermediate19 Project. Enter your C++ instructions into a source file named Intermediate19.cpp. Also enter appropriate comments and any additional instructions required by the compiler.
  - e. Save and then run the program. Test the program using the same data used to desk-check the program.

- 20. The sales manager at Tompkins Company wants a program that calculates and displays each salesperson's commission, which is 10% of his or her sales. It should also display the commission. Use a value-returning function to get the amount sold by a salesperson. The amount sold may contain a decimal place. Also use three functions: one to calculate the 10% commission, another to display the commission, and another to calculate the total commission. The program should display the commission and total commission in fixed-point with two decimal places. Display the total commission only after the sales has finished the amounts. Use a sentinel value to end the program.
  - a. Create IPO charts for the problem.
  - b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier in Figure 10-35. Then, code the algorithm into a program.
  - c. If necessary, create a new project Intermediate20 Project. Enter your C++ instructions into a source file named Intermediate20.cpp. Also enter appropriate comments and any additional instructions required by the compiler.
  - d. Save and run the program. Test the program using the following sales amounts: 1200, 2300, 1000, and 2500. Enter your sentinel value.

- 21. In this exercise, you create a program that calculates the average of three test scores. The program should contain two value-returning functions (getTestScores and calAverage) and two void functions. The main function should call the void getTestScores function to get three test scores. The test may contain a decimal place. The main function should then call the value-returning calAverage function to calculate the average of the test scores. When calAverage function has completed its task, the main function should call the void displayAverage function to display the average of the test scores on the screen. Display the average with one decimal place. Use a sentinel value to end the program.
  - a. Create IPO charts for the problem, and desk-check the algorithm using the four sets of test scores followed by your sentinel value: 56, 78, 90; 100, 85, 67; 74, 32, 98; and 25, 99, 84.
  - b. List the input, processing, and output items, as well as the algorithm, in a chart similar to the one shown earlier in Figure 10-35. Then, code the algorithm into a program.
  - c. Desk-check the program using the same data to desk-check the algorithm.
  - d. If necessary, create a new project Advanced21 Project. Enter your C++ instructions into a source file named Advanced21.cpp. Also enter appropriate comments and any additional instructions required by the compiler.
  - e. Save and run the program. Test the program using the same data used to desk-check the program.

- 22. In this exercise, you prevent a function from changing the value of a named constant passed to it.
  - a. If necessary, create a new project named Advanced22 Project. Copy the instructions from Lab10-2.cpp file into a source file named Advanced22.cpp. (Alternatively, you can enter the instructions from Figure 10-31 into the Advanced22.cpp file) Change the filename in the first comment to Advanced22.cpp.
  - b. The program passes the value of UNIT_CHG named constant to the calcBill function, which stores the value in the chgPerUnit variable. Because the function stores in a value, it can be changed by the function. First, you will verify that the calcBill function can change the value stored in the chgPerUnit variable. Insert a blank line above the chgPerUnit; statement in the calcBill function. In the blank line, type `chgPerUnit = .25;` Save and run the program. Enter 3000 and 2000 to see the current and previous readings. The program displays 100 as the number of units used, which is correct. However, rather than displaying $90.00 as the total charge, the program displays $250.00.
  - c. To prevent the calcBill function from changing the charge per unit, you must use the const keyword to indicate that the value being passed is a constant. Make the appropriate modification to the calcBill function's prototype and its header. Save and run the program. The compiler displays an error message that you cannot assign a value to the chgPerUnit variable, which is defined using the const keyword.
  - d. Delete the `chgPerUnit = .25;` statement from the calcBill function. Save and run the program. Enter 3000 and 2000 to see the current and previous readings. The program correctly displays 1000 and $90.00 as the units used and total charge, respectively.

- 23. In this exercise, you modify the electric bill from Lab10-2.
  - a. If necessary, create a new project named Advanced23 Project. Copy the instructions from the Lab10-2.cpp file into a source file named Advanced23.cpp. (Alternatively, you can enter the instructions from Figure 10-31 into the Advanced23.cpp file) Change the filename in the first comment to Advanced23.cpp.
  - b. Modify the program so that it allows the user to display the electric bill for more than one customer without having to run the program. Use a sentinel value to end the program. The sentinel value should be entered as the current meter reading in the `getInput` function. When the user enters the sentinel value, the `getInput` function should not prompt the user to enter the previous
