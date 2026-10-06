# Following are some characteristics of an infinite loop:

+   1. No termination condition is specified.
2. The specified conditions never meet.

The specified condition determines whether to execute the loop body or not. 'C' programming language provides us with three types of loop statements (constructs):

+   1. The while loop
2. The do-while loop
3. The for loop

# while loop

A loop is an entry-controlled loop. In while loop, a condition is evaluated before processing a body of the loop. If a condition is true, then and only then the body of a loop is executed. After the body of a loop is executed, then control goes back at the beginning, and the condition is checked if it is true, the same process is executed until the condition becomes false. Once the condition becomes false, control goes out of the loop.

After exiting the loop, the control goes to the statements which are immediately after the loop. The body of a loop can contain more than one statement. If it contains only one statement, then the curly braces are not compulsory. It is a good practice though to use the curly braces even we have a single statement in the the body.

In while loop, if the condition is not true, then the body of a loop will not be executed, not even once. It is different in while loop which we will shortly.

# How while loop works?

+   * The while loop evaluates the test expression inside the parenthesis ().
* If the test expression is true, statements inside the body of while loop are executed. Then, the test expression is evaluated again.
* The process goes on until the test expression is evaluated to false.
* If the test expression is false, the loop terminates (ends).