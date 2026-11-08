**Sample Run:** In this sample run, the user input is shaded.

```
Program to convert uppercase letters to their corresponding telephone digits.
To stop the program enter #.
Enter a letter: A
The letter you entered is: A
The corresponding telephone digit is: 2

Enter another uppercase letter to find its corresponding telephone digit.
To stop the program enter #.
Enter a letter: D
The letter you entered is: D
The corresponding telephone digit is: 3

Enter another uppercase letter to find its corresponding telephone digit.
To stop the program enter #.
Enter a letter: #
```

This program works as follows. The statements in Lines 2 and 3 tell the user what to do. The statement in Line 4 prompts the user to input a letter; the statement in Line 5 reads and stores that letter into the variable letter. The while loop in Line 7 checks that the letter is #. If the letter entered by the user is not #, the body of the while loop executes. The statement in Line 8 outputs the letter entered by the user. The if statement in Line 10 checks whether the letter entered by the user is uppercase. The statement of the if statement is the switch statement (Line 11). If the letter entered by the user is uppercase, the expression in the if statement (in Line 11) evaluates to true and the switch statement executes; if the letter entered by the user is not uppercase, the else statement (Line 27) executes. The statements in Lines 12 through 26 determine the corresponding telephone digit.

Once the current letter is processed, the statements in Lines 29 and 30 again inform the user what to do next. The statement in Line 31 prompts the user to enter a letter; the statement in Line 32 reads and stores that letter into the variable letter. (Note that the statement in Line 29 is similar to the statement in Line 2 and that the statements in Lines 30 through 33 are the same as the statements in Lines 3 through 6.) After the statement in Line 33 (at the end of the while loop) executes, the control goes back to the top of the while loop and the same process begins again. When the user enters #, the program terminates.

Notice that in this program, the variable letter is the loop control variable. First, it is initialized in Line 5 by the input statement, and then it is updated in Line 32. The expression in Line 7 checks whether letter is #.

> > **NOTE:** In the program in Example 5-5, you can write the statements between Lines 10 and 28 using a switch statement. (See Programming Exercise 3 at the end of this chapter.)

# Case 3: Flag-Controlled while Loops

A **flag-controlled while loop** uses a bool variable to control the loop. Suppose found is a bool variable. The flag-controlled while loop takes the following form: