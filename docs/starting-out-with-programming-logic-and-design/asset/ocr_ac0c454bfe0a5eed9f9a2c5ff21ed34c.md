# Chapter 6 Functions

Line 3 declares the variables to hold the sales, the commission rate, and the amount of advanced pay. Line 6 calls the getSales function, which gets the amount of sales from the user and returns that value. The value that is returned from the function is assigned to the sales variable. Line 9 calls the getAdvancedPay function, which gets the amount of advanced pay from the user and returns that value. The value that is returned from the function is assigned to the advancedPay variable.

Line 12 calls the determineCommissionRate function, passing sales as an argument. This function returns the rate of commission for the amount of sales. That value is assigned to the commissionRate variable. Line 15 calculates the amount of pay, and then line 18 displays that amount. The If-then statement in lines 21 through 24 determines whether the pay is negative, and if so, displays a message indicating that the salesperson must reimburse the company. Figure 6-11 shows a flowchart for the main module.

# Figure 6-11 Flowchart for the main module

![](bbox=[0.121, 0.383, 0.839, 0.881])

The getSales function definition is next.