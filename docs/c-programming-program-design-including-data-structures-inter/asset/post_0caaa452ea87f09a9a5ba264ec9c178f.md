
program closely, we can see that the four lines are produced because the outer loop executes four times. The values assigned to loop control variable i are 1, 2, 3, and 4. This is an example of the classic “off-by-one” problem. (In an “off-by-one problem,” either the loop executes one too many or one too few times.) We can eliminate this problem by correctly setting the values of the loop control variable. For example, we can rewrite the loops as follows:

```cpp
for (i = 1; i <= 3; i++)
{
    sum = 0;

    for (j = 1; j <= 4; j++)
    {
        infile >> num;
        cout << num << " ";
        sum = sum + num;
    }

    cout << "sum = " << sum << endl;
}
```

This code fixes the original problem without using a software patch. It also represents good programming practice. The complete modified program is available at the Web site accompanying this book and is named Ch5_LoopWithBugsCorrectedProgram.cpp.

## Debugging Loops

As we have seen in the earlier debugging sections, no matter how careful a program is designed and coded, errors are likely to occur. If there are syntax errors, the compiler will identify them. However, if there are logical errors, we must carefully look at the code or even maybe at the design and try to find the errors. To increase the reliability of the program, errors must be discovered and fixed before the program is released to the users.

Once an algorithm is written, the next step is to verify that it works properly. If the algorithm is a simple sequential flow or contains a branch, it can be hand traced or you can use the debugger, if any, provided by the IDE. Typically, loops are harder to debug. The correctness of a loop can be verified by using loop invariants. A loop invariant is a set of statements that remains true each time the loop body is executed. Let p be a loop invariant and q be the (logical) expression in a loop statement. Then p && q remains true before each iteration of the loop and p && not(q) is true after the loop terminates. The full discussion of loop invariants is beyond the scope of the book. However, you can learn about loop invariants in the book: *Discrete Mathematics: Theory and Applications* (Revised Edition), D.S. Malik and M.K. Sen, Cengage Learning Asia, Singapore, 2010. Here, we give a few tips that you can use to debug a loop.

As discussed in the previous section, the most common error associated with loops is off-by-one. If a loop turns out to be an infinite loop, the error is most likely in the logical expression that controls the execution of the loop. Check the logical expression carefully and see if you have reversed an inequality, an assignment statement symbol appears in place of the equality operator, or && appears in place of ||. If the loop changes the values of variables, you can print the values of the variables before and/or after each iteration or you can use your IDE's debugger, if any, and watch the values of variables during each iteration.

The debugging sections in this book are designed to help you understand the debugging process. However, as you will realize, debugging can be a tiresome process. If your program is very bad, do not debug. Throw it away and start over.

## QUICK REVIEW

- 1. C++ has three looping (repetition) structures: `while`, `for`, and `do...while`.
- 2. The syntax of the `while` statement is:

    ```cpp
    while (expression)
        statement
    ```

- 3. In C++, `while` is a reserved word.
- 4. In the `while` statement, the parentheses around the expression (the decision maker) are important; they mark the beginning and end of the expression.
- 5. The statement is called the body of the loop.
- 6. The body of the `while` loop must contain a statement that eventually sets the expression to `false`.
- 7. A counter-controlled `while` loop uses a counter to control the loop.
- 8. In a counter-controlled `while` loop, you must initialize the counter before the loop, and the body of the loop must contain a statement that changes the value of the counter variable.
- 9. A sentinel is a special value that marks the end of the input data. The sentinel must be similar to, yet differ from, all the data items.
- 10. A sentinel-controlled `while` loop uses a sentinel to control the `while` loop. The `while` loop continues to execute until the sentinel is read.
- 11. An EOF-controlled `while` loop continues to execute until the program detects the end-of-file marker.
- 12. In the Windows console environment, the end-of-file marker is entered using Ctrl+Z (hold the Ctrl key and press z). In the UNIX environment, the end-of-file marker is entered using Ctrl+D (hold the Ctrl key and press d).
- 13. A `for` loop simplifies the writing of a counter-controlled `while` loop.
- 14. In C++, `for` is a reserved word.
- 15. The syntax of the `for` loop is:

    ```cpp
    for (initialize statement; loop condition; update statement)
        statement
    ```

    statement is called the body of the `for` loop.
- 16. Putting a semicolon at the end of the `for` loop (before the body of the `for` loop) is a semantic error. In this case, the action of the `for` loop is empty.
- 17. The syntax of the `do...while` statement is:

    ```cpp
    do
        statement;
    while (expression);
    ```

    statement is called the body of the `do...while` loop.
- 18. Both `while` and `for` loops are called pretest loops. A `do...while` loop is called a posttest loop.
- 19. The `while` and `for` loops may not execute at all, but the `do...while` loop always executes at least once.
- 20. Executing a `break` statement in the body of a loop immediately terminates the loop.
- 21. Executing a `continue` statement in the body of a loop skips the loop’s remaining statements and proceeds with the next iteration.
- 22. When a `continue` statement executes in a `while` or `do...while` loop, the expression update statement in the body of the loop may not execute.
- 23. After a `continue` statement executes in a `for` loop, the update statement is the next statement executed.

## EXERCISES

- 1. Mark the following statements as true or false.

  - a. In a counter-controlled `while` loop, it is not necessary to initialize the loop control variable.
  - b. It is possible that the body of a `while` loop may not execute at all.
  - c. In an infinite `while` loop, the `while` expression (the decision maker) is initially false, but after the first iteration it is always true.
  - d. The `while` loop:

        ```cpp
        j = 0;
        while (j <= 10)
            j++;
        ```

        terminates if `j > 10`.
  - e. A sentinel-controlled `while` loop is an event-controlled `while` loop whose termination depends on a special value.
  - f. A loop is a control structure that causes certain statements to execute over and over.
  - g. To read data from a file of an unspecified length, an EOF-controlled loop is a good choice.

- 7. Suppose that the input is 25 36 18 16 −1. What is the output of the following code?

    ```cpp
    int num;
    int sum;
    cin >> sum;
    num = sum;

    while (num != -1)
    {
        cin >> num;
        sum = sum + num;
    }
    cout << "Sum = " << sum << endl;
    ```

- 8. Suppose that the input is 25 36 18 16 −1. What is the output of the following code?

    ```cpp
    int num;
    int sum;

    cin >> num;
    sum = num;

    while (num != -1)
    {
        sum = sum + num;
        cin >> num;
    }
    cout << "Sum = " << sum << endl;
    ```

- 9. Suppose that the input is 10 −6 12 −5 −4 0. What is the output of the following code?

    ```cpp
    int num;
    int sum = 0;

    cin >> num;

    while (num != 0)
    {
        if (num > 0)
            sum = sum + num;
        else
            sum = sum - num;
        cin >> num;
    }
    cout << "Sum = " << sum << endl;
    ```

- 10. Correct the following code so that it reads and finds the sum of 20 numbers:

    ```cpp
    int count = 0;
    int sum = 0;

    cin >> num;
    while (count <= 20);
    ```
