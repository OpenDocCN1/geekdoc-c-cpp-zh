# Using a Pretest Loop to Solve a Real-World Problem

Now consider the Miller Incorporated problem specification and IPO chart, which are shown in Figure 7-4. The problem specification is similar to the one foring and indicates that the program will need to calculate and display the bonus for more than one employee. You could use the algorithm shown in Figure 7-3 to solve the Miller Incorporated problem; however, that is inefficient for the current problem. A program based on the algorithm in Figure 7-3 would need to be executed once for each salesperson receiving a bonus. In other words, if Miller Incorporated had 100 salespeople, the payroll clerk would need to run the program 100 times. The Miller Incorporated problem specification, you will notice, that the payroll clerk wants to calculate and display each salesperson's bonus without having to run the program more than once. To accomplish this, the algorithm will need a repetition structure, as shown in Figure 7-4. After running a program based on the algorithm in Figure 7-4, the payroll clerk can calculate and display the bonus amount for any number of salespeople. The program will end when the payroll clerk enters -1 (a negative number) as the sales amount.

# Problem specification

In January of each year, Miller Incorporated pays a 5% bonus to each of salespeople. The bonus is based on the amount of sales made by the salesperson during the previous year. The payroll clerk wants a program that calculates and displays the bonus amounts for as many salespeople as needed without having to run the program more than once. Because the sales amounts entered by the payroll clerk will always be positive numbers, the payroll clerk will indicate that he is finished with the program by entering a sales amount of -1 (a negative number 1).

| Input | Processing | Output |
| --- | --- | --- |
| bonus rate (5%) sales | Processing items: none | bonus | calculates and displays the bonus for as many salespeople as needed |

```
Algorithm:
1. enter the sales
2. repeat (while the sales are not equal to -1)
   calculate the bonus by multiplying the sales by
   the bonus rate
   display the bonus
   enter the sales
repeat
```

Figure 7-4 Problem specification and IPO chart for the Miller Incorporated program