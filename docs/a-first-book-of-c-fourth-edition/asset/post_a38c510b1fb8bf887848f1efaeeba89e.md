
## Figure 5.8 The do statement's flow of control

As shown, all statements within the do-while statement are executed at least once before the expression is evaluated. Then, if the expression has a non-zero value, the statements are executed again. This process continues until the expression evaluates to zero (becomes false). For example, take a look at the following do-while statement:

```
do
{
    cout << "\nEnter a price: ";
    cin >> price;
    if ( abs(price - SENTINEL) < 0.0001 ) break;
    salestax = RATE * price;
    cout << "The sales tax is $" << salestax;
}
while (price != SENTINEL);
```

Observe that only one prompt and cin statement are used because the tested expression is evaluated at the end of the loop.

As with all repetition statements, the do-while statement can always replace or be replaced by an equivalent while or for statement. The choice of which statement to use depends on the application and the programmer’s preferred style. In general, while and for statements are preferred because anyone reading the program can clearly see what’s being tested up front, at the top of the program loop.

## Validity Checks

The do-while statement is particularly useful in filtering user-entered input and providing data validation checks. For example, an operator is required to enter a valid customer identification number between 100 and 1999. A number outside this range is rejected, and a new request for a valid number is made. The following section of code supplies the data filter needed to verify the entry of a valid identification number:

```
do
{
    cout << "\nEnter an identification number: ";
    cin  >> idNum;
}
while (idNum < 100 || idNum > 1999);
```

In this code, a request for an identification number is repeated until a valid number is entered. This section of code is “bare bones,” in that it doesn’t alert the operator to the cause of the new request for data or allow premature exit from the loop if a valid identification number can’t be found. The following code is an alternative for removing the first drawback:

```
do
{
    cout << "\nEnter an identification number: ";
    cin  >> idNum;
    if (idNum < 100 || idNum > 1999)
    {
        cout << "\n An invalid number was just entered"
             << "\nPlease check the ID number and reenter";
    }
    else
        break;     // break if a valid ID number was entered
} while(1);         // this expression is always true
```

A break statement is used to exit from the loop. Because the expression the do-while statement is evaluating is always 1 (true), an infinite loop has been created that’s exited only when the break statement is encountered.

## EXERCISES 5.4

- 1. (Program) a. Using a do-while statement, write, compile, and run a C++ program to accept a grade. The program should request a grade continuously as long as an invalid grade is entered. An invalid grade is any grade less than 0 or greater than 100. After a valid grade has been entered, your program should display the value of the grade entered.
  b. Modify the program written for Exercise 1a so that the user is alerted when an invalid grade has been entered.
  c. Modify the program written for Exercise 1b so that it allows the user to exit the program by entering the number 999.
  d. Modify the program written for Exercise 1b so that it automatically terminates after five invalid grades are entered.

- 2. (Program) a. Write, compile, and run a C++ program that continuously requests a grade to be entered. If the grade is less than 0 or greater than 100, your program should print a message informing the user that an invalid grade has been entered; else, the grade should be added to a total. When a grade of 999 is entered, the program should exit the repetition loop and compute and display the average of the valid grades entered.
  b. Run the program written in Exercise 2a on a computer and verify the program by using appropriate test data.

- 3. (Program) a. Write, compile, and run a C++ program to reverse the digits of a positive integer number. For example, if the number 8735 is entered, the number displayed should be 5378.
  (Hint: Use a do-while statement and continuously strip off and display the number's units digit. If the variable num initially contains the number entered, the units digit is obtained as (num % 10).). After a units digit is displayed, dividing the number by 10 sets up the number for the next iteration. Therefore, (8735 % 10) is 5 and (8735 / 10) is 873. The do-while statement should continue as long as the remaining number is not 0.
  b. Run the program written in Exercise 3a on a computer and verify the program by using appropriate test data.

- 4. (Practice) Repeat any of the exercises in Section 5.3, using a do-while statement rather than a for statement.

## 5.5 Common Programming Errors

When using repetition statements, beginning C++ programmers are prone to making the following seven errors:

- 1. The most troublesome error for new programmers is the "off by one" error, in which the loop executes one too many or one too few times than was intended. For example, the loop created by the statement for(i = 7; i < 11; i++) executes 10 times, not 11, even though the number 11 is used in the statement. An equivalent loop can be constructed by using the statement for(i = 1; i <= 10; i++).

However, if the loop is started with an initial value of i = 0, using the statement for(i = 0; i < 11; i++), the loop is traversed 11 times, as is a loop constructed with the statement for(i = 0; i <= 10; i++). In constructing loops, you must pay particular attention to both the initial and final conditions used to control the loop to make sure the number of loop traversals isn't off by one too many or one too few executions.

The next two errors pertain to the tested expression, and you have already encountered them with the if and switch statements:

- 2. Inadvertently using the assignment operator, =, in place of the equality operator, ==, in the tested expression—for example, typing the assignment expression a = 5 instead of the correct relational expression a==5. Because the tested expression can be any valid C++ expression, including arithmetic and assignment expressions, the compiler doesn't detect this error.

- 3. Using the equality operator, ==, when testing double-precision operands. For example, the expression fnum == 0.01 should be replaced by a test requiring that the absolute value |fnum - 0.01| be less than an acceptable amount. The reason is that all numbers are stored in binary form. Using a finite number of bits, decimal numbers such as 0.01 have no exact binary equivalent, so tests requiring equality with these numbers can fail. (See Section 4.1 for a more complete description of this numerical accuracy problem.)

The next three errors are particular to the for statement:

- 4. Placing a semicolon at the end of for's parentheses, which often produces a do-nothing loop. For example, take a look at these statements:

  for(count = 0; count < 10; count++);
      total = total + num;

  The semicolon at the end of the first line of code is a null statement. It has the effect of creating a loop that's executed 10 times with nothing done except incrementing and testing count. This error tends to occur because C++ programmers are used to ending most lines with a semicolon.

- 5. Using commas to separate items in a for statement instead of the required semicolons, as in this example:

  for (count = 1, count < 10, count++)

  Commas must be used to separate items in the initializing and altering lists, but semicolons must be used to separate these lists from the tested expression.

- 6. Changing the value of the control variable used in the tested condition both inside the body of a for loop and in its altering list. For example, take a look at this for loop:

  for(int i=0; i<10; i++)
      cout << i++;

  In this code, the value of the variable being tested (in this case, i) is changed in two places, which is a serious logic error.
