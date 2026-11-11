The for loop first performs initialization of the variable(s) specified in initialization part of its syntax. After initialization is completed, the loop checks for the result of condition specified. Only if the condition is evaluated as ‘true’, operations within the loop will be executed. After the specified operations are fully executed, the loop performs ‘increment/decrement’. After performing ‘increment/decrement’, the condition is again evaluated to determine if execution of operation must be repeated. In summary, the execution of operation is repeated as long as the condition is evaluated as ‘true’. The control is transferred inside the body of the loop only if condition is true hence for loop is also **entry control type of loop**, similar to a while loop.

If the condition is evaluated as ‘false’, the execution of loop terminates and the control is transferred to the first statement outside the body of the loop.

Figure 5.12 illustrates the working of for loop in detail, followed by examples to understand for loop:

> **NOTES**
> 
> **For loop** is also a **entry control loop** like `while` loop.
> 
> The syntax of for loop is simple and it helps improve the **readability of the program** when compared to while loop.

![](bbox=[0.277, 0.455, 0.744, 0.772])

**Figure 5.12:** Working of for loop

# 5.3.1 Program to compute the series 1² + 2² + 3² + 4² + . . . x² using for loop: An example

As seen, the series starts from 1 and ends at a value x. The end value x is required to be configurable and will be taken as input from the user. Similar to all the examples discussed earlier, we will use a counting variable k that will take all the values from 1 to x step