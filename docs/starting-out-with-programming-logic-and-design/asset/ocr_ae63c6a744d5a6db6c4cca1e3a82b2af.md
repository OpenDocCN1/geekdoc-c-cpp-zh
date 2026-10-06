# Chapter 5

As shown in Program 5-5, the commission calculating program can be easily modified to use a Do-While loop instead of a While loop. Notice that in this version of the program, line 3, we do not initialize the keepGoing variable with the string "y". It isn't necessary because the Do-While loop, in lines 7 through 15, will always execute at least once. This means that the Input statement in line 14 will always execute a value before the condition is tested in line 15.

Figure 5-8 shows a flowchart for the main module.

# Program 5-5

```
Module main()
  // Local variable
  Declare String keepGoing

  // Calculate commissions as many
  times as needed.
  Do
    // Display a salesperson's commission.
    Call showCommission()
    // Do it again?
    Display "Do you want to calculate another"
    Display "Commission? (Enter y for yes)"
    Input keepGoing
  While keepGoing == "y"
End Module

\  // The showCommission module gets the
  // amount of sales and displays the
  // commission.
Module showCommission()
  // Local variables
  Declare Real sales, commission

  // Constant for the commission rate
  Constant Real COMMISSION_RATE = 0.10

  // Get the amount of sales.
  Display "Enter the amount of sales"
  Input sales

  // Calculate the commission.
  Set commission = sales * COMMISSION_RATE

  // Display the commission
  Display "The commission is $", commission
End Module
```

The output of this program is the same as that of Program 5-1