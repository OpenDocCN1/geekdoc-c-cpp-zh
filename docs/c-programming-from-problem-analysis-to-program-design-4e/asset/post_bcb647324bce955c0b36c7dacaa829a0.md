
## EXAMPLE 6.19

```
int total = 0;
for (int nValue = 0; nValue < 10; nValue++)
{
    if (nValue % 2 == 0)
    {
        continue;
    }
    total += nValue;
    Console.Write(nValue + "\t");
}
Console.WriteLine("\nTotal is equal to {0}.", total);
```

The output for this code is:

```
1      3      5      7      9
Total is equal to 25.
```

Note that the difference between the break and continue statements is that the continue statement does not stop the execution of the loop body, but rather, halts that iteration and transfers control to the next iteration of the loop.

The other jump statements in C# are goto, throw, and return. You will learn about the throw statement with exception handling in Chapter 12. You have used the return statement in your value-returning methods. The goto statement transfers control to a statement that is marked by a label. The goto statement has a bad reputation. It is associated with poorly designed spaghetti code that is difficult to debug and maintain. You should not use a goto jump statement in your programs.

The break and continue statements should also be used sparingly. It is appropriate and a requirement that you use a break statement with a switch statement. However, when you use break and continue statements with a loop, you are violating the single entry and single exit guideline for developing a loop. What this means is that there should be only one way to enter a loop and one way to exit. When you exit a loop from multiple locations, it becomes more difficult to debug. The loop might end because the condition evaluates to false or it might end prematurely because of the break. This adds complications when you are trying to walk through the logic.

## Deciding Which Loop to Use

The decision regarding which type of loop to use is sometimes a personal choice; however, there are some considerations you might want to acknowledge and allow to overrule your personal biases. Remember that the body of the do...while is always executed at least once. Thus, you should avoid using this form if there is the possibility that the loop body should not be executed when certain types of data are input into your program. Conversely, if you know your loop will always be executed at least once, the do...while is a good option.

If a numeric variable is being changed by a consistent amount with each iteration through the loop, the compactness of the for statement might work best. The initialization, conditional expression, and update can all be located on the same line. Although the format allows for multiple entries for all three of these entries, a good rule of thumb is that the for statement initialization, condition, and update should be able to be placed on one line. Remember, readability is always an important consideration.

The while statement can be used to write any type of loop. It can implement counter-controlled loops just as the for statement can. The while statement is also useful for applications requiring state- and sentinel-controlled loops. So it is always a good option. It offers the advantage of being a pretest type. With all of the loops, you want to ensure that you understand and design the condition that is used to end the loop as well as how the condition is updated or changed.

## PROGRAMMING EXAMPLE: LoanApplication

This example demonstrates the use of loops in the analysis, design, and implementation of a program. Both pretest and posttest forms of loops are included in the example. The pretest form is used to calculate individual loan details. It is nested inside the posttest through method calls. Static and instance methods, properties, and selection statements are included. Figure 6-16 outlines the problem specification.

Create an application that will allow a loan amount, interest rate, and number of finance years to be entered for a given loan. Determine the monthly payment amount. Calculate how much interest will be paid over the life of the loan. Display an amortization schedule showing the new balance after each payment is made.

Design an object-oriented solution. Use two classes. For the Loan class, characteristics such as the amount to be financed, rate of interest, period of time for the loan, and total interest paid will identify the current state of a loan object. Include methods to determine the monthly payment amount, return the total interest paid over the life of the loan, and return an amortization schedule.

In the second class, instantiate an object of the loan class. Allow the user to input data about more than one loan. Display in the LoanApp class the payment amount, amortization schedule, and the total amount of interest to be paid.

**FIGURE 6-16 Problem specification for the LoanApplication example**

### ANALYZE THE PROBLEM

You should review the problem specification in Figure 6-16, and make sure you understand the problem definition. Several values are put into the program to represent the loan amount, rate, and the time period of the loan. These values are entered as string variables and then parsed or converted into numeric fields so that the calculations can be performed.

Two separate classes are to be developed. Creating a separate class for the Loan object enables the class to be used by other applications. The class includes an algorithm for producing an amortization schedule. It also includes a stand-alone method to determine the total interest paid over the life of the loan.

### DATA

Tables 6-3 and 6-4 list the data field members needed for the LoanApplication problem.

**TABLE 6-3 Instance field members for the Loan class**

| Data item description | Type | Identifier |
|---|---|---|
| Amount of loan | double | loanAmount |
| Interest rate | double | rate |
| Total interest paid | double | totalInterestPaid |
| Monthly payment amount | double | paymentAmount |
| Current balance of the loan | double | balance |
| Current amount paid toward principal | double | principal |
| Number of payments | int | numPayments |
| Interest for the current month | double | monthInterest |

The client class that is using the Loan class will need additional data. As noted in the problem specification, the client or application class allows the user to enter values for the loan. Table 6-4 identifies some of the local variables needed by the application class.

**TABLE 6-4 Local variables for the LoanApp class**

| Data item description | Type | Identifier |
|---|---|---|
| Amount of loan | double | loanAmount |
| Interest rate | double | interestRate |
| Number of years to finance loan | int | years |
| More calculations (loop state-controlled variable) | char | anotherLoan |

The top three entries in Table 6-4 will be used to instantiate an object of the Loan class. After the values are entered and converted to numeric values, the loan constructor will be called to create a Loan object.

### CONSTANTS

No constants are used for this application.

### FORMULAS

Formulas are needed to calculate the following:

1. numPayments = years * 12
2. term = (1 + rate / 12.0)^numPayments
3. paymentAmount = loanAmount * rate / 12 * term / (term - 1.0)
4. monthInterest = rate / 12 * balance
5. principal = payment - monthInterest
6. balance = balance - principal
7. totalInterestPaid = totalInterestPaid + monthInterest

### DESIGN A SOLUTION

The desired output is to display the monthly payment amount, an amortization schedule, and the total interest paid over the life of the loan. Figure 6-17 shows a prototype for the final output. The xxx's are placed in the prototype to represent the location in which the calculated values should appear.

**FIGURE 6-17 Prototype for the LoanApplication example**

![](img/36e48639a06772bcb0fa1ea2525b33a3_399_0.png)

The object-oriented approach focuses on the object. The loan application has both data and behavior characteristics that can be identified. Class diagrams are used to help design and document these characteristics. Figure 6-18 shows the class diagrams for the Loan Application example.

![](img/36e48639a06772bcb0fa1ea2525b33a3_399_1.png)

**FIGURE 6-18 Class diagrams**
