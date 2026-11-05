If a numeric variable is being changed by a consistent amount with each iteration through the loop, the compactness of the for statement might work best. The initialization, conditional expression, and update can all be located on the same line. Although the format allows for multiple entries for all three of these entries, a good rule of thumb is that the for statement initialization, condition, and update should be able to be placed on one line. Remember, readability is always an important consideration.

The while statement can be used to write any type of loop. It can implement counter-controlled loops just as the for statement can. The while statement is also useful for applications requiring state- and sentinel-controlled loops. So it is always a good option. It offers the advantage of being a pretest type. With all of the loops, you want to ensure that you understand and design the condition that is used to end the loop as well as how the condition is updated or changed.

# PROGRAMMING EXAMPLE: LoanApplication

This example demonstrates the use of loops in the analysis, design, and implementation of a program. Both pretest and posttest forms of loops are included in the example. The pretest form is used to calculate individual loan details. It is nested within the iteration through several loans. Posttest and nested methods, pretest, and selection statements are included. Figure 6-16 outlines the problem specification.

Create an application that will allow a loan amount, interest rate, and number of finance years to be entered for a given loan. Determine the monthly payment amount. Calculate how much interest will be paid over the life of the loan. Display an amortization schedule showing the new balance after each payment is made.

Design an object-oriented solution. Use two classes. For the Loan class, characteristics such as the amount to be financed, rate of interest, period of time for the loan, and total interest paid will identify the current state of a loan object. Include methods to determine the monthly payment amount, return the total interest paid over the life of the loan, and return an amortization schedule.

In the second class, instantiate an object of the loan class. Allow the user to input data about more than one loan. Display in the LoanApp class the payment amount, amortization schedule, and the total amount of interest to be paid.

FIGURE 6-16 Problem specification for the LoanApplication example

Programming Examples are complete programs featured at the end of the chapter. The examples contain the distinct stages of preparing a problem specification, analyzing the problem, designing the solution, and coding the implementation.