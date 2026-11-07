```
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed 9
Failed 1
Bonus to instructor!
```

**Fig. 4.16** | Examination-results problem: Nested control statements. (Part 2 of 2.)

declarations (passes is initialized to 0, failures is initialized to 0 and studentCounter is initialized to 1). Looping programs may require initialization at the beginning of each repetition; such reinitialization normally would be performed by assignment statements rather than in declarations or by moving the declarations inside the loop bodies.

The while statement (lines 15–29) loops 10 times. Each iteration inputs and processes one exam result. The if...else statement (lines 22–25) for processing each result is nested in the while statement. If the result is 1, the if...else statement increments passes; otherwise, it assumes the result is 2 and increments failures. Line 28 increments studentCounter before the loop condition is tested again in line 15. After 10 values have been input, the loop terminates and line 32 displays the number of passes and the number of failures. The if statement in lines 35–36 determines whether more than eight students passed the exam and, if so, outputs the message "Bonus to instructor!".

Figure 4.16 shows the input and output from two sample executions of the program. At the end of the second sample execution, the condition in line 35 is true—more than eight students passed the exam, so the program outputs a message indicating that the instructor should receive a bonus.

# 4.11 Assignment Operators

C++ provides several assignment operators for abbreviating assignment expressions. For example, the statement

```
c = c + 3;
```

can be abbreviated with the addition assignment operator += as

```
c += 3;
```

which adds the value of the expression on the operator’s right to the value of the variable on the operator’s left and stores the result in the left-side variable. Any statement of the form

```
variable = variable operator expression;
```

in which the same variable appears on both sides of the assignment operator and operator is one of the binary operators +, -, *, /, or % (a few others we’ll discuss later in the text), can be written in the form

```
variable operator= expression;
```