# Program Testing

An important technique in testing a program is to test all kinds of input. There is no precise definition of what we mean by a “kind” of input, but in practice, it is often easy to decide what kinds of input data a program deals with. In the case of our supermarket program, there are two main kinds of input: input that uses the low markup of 5 percent and input that uses the high markup of 10 percent. Thus, we should test at least one case in which the item is expected to remain on the shelf for less than 7 days and at least one case in which the item is expected to remain on the shelf for more than 7 days.

Another testing strategy is to test boundary values. Unfortunately, boundary value is another vague concept. An input (test) value is a boundary value if it is a value at which the program changes behavior. For example, in our supermarket program, the program’s behavior changes at an expected shelf stay of 7 days. Thus, 7 is a boundary value; the program behaves differently for a number of days that is less than or equal to 7 than it does for a number of days that is greater than 7. Hence, we should test the program on at least one case in which the item is expected to remain on the shelf for exactly 7 days. Normally, you should also test input that is one step away from the boundary value as well, since you can easily be off by one in deciding where the boundary is. Hence, we should test our program on input for an item that is expected to remain on the shelf for 6 days, an item that is expected to remain on the shelf for 7 days, and an item that is expected to remain on the shelf for 8 days. (This is in addition to the test inputs described in the previous paragraph, which should be well below and well above 7 days.)

# SELF-TEST EXERCISES

+   13. Can a function definition appear inside the body of another function definition?
+   
+   14. Can a function definition contain a call to another function?
+   
+   15. Rewrite the function declaration comment for the function order shown in Display 5.8 so that it is expressed in terms of preconditions and postconditions.
+   
+   16. Give a precondition and a postcondition for the predefined function `sqrt`, which returns the square root of its argument.

# 5.4  TESTING AND DEBUGGING FUNCTIONS

> “I beheld the wretch—the miserable monster whom I had created.”
> 
> MARY WOLLSTONECRAFT SHELLEY, *Frankenstein*