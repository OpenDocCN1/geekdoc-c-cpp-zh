Sample data are shown below:

```
250 5750
100 28000
50 35750
25 18570
```

The first line indicates that the ticket price is $250 and that 5750 tickets were sold at that price. Output the number of tickets sold and the total sale amount. Format your output with two decimal places.

+   6. Redo Programming Exercise 21, in Chapter 2, so that each string can store a line of text.

+   7. Three employees in a company are up for a special pay increase. You are given a file, say `Ch3_Ex7Data.txt`, with the following data:

```
Miller Andrew 65789.87 5
Green Shiloh 75892.56 6
Sethi Amit 74900.50 6.1
```

Each input line consists of an employee's last name, first name, current salary, and percent pay increase. For example, in the first input line, the last name of the employee is Miller, the first name is Andrew, the current salary is 65789.87, and the pay increase is 5%. Write a program that reads data from the specified file and stores the output in the file `Ch3_Ex7Output.dat`. For each employee, the data must be output in the following form:

`firstName lastName updatedSalary`. Format the output of decimal numbers to two decimal places.

+   8. Write a program that accepts as input the mass, in grams, and density, in grams per cubic centimeters, and outputs the volume of the object using the formula: `volume = mass / density`. Format your output to two decimal places.

+   9. Interest on a credit card’s unpaid balance is calculated using the average daily balance. Suppose that `netBalance` is the balance shown in the bill, `payment` is the payment made, `d1` is the number of days in the billing cycle, and `d2` is the number of days payment is made before billing cycle. Then, the average daily balance is:

$$averageDailyBalance = \frac{netBalance * d1 - payment * d2}{d1}$$

If the interest rate per month is, say, 0.0152, then the interest on the unpaid balance is:

$$interest = averageDailyBalance * 0.0152$$