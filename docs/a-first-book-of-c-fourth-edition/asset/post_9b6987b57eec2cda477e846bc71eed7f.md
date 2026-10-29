
$18.00 for each hour worked over 40 hours. The program should request the hours worked as input and display the salary as output.

b. How many runs should you make for the program written in Exercise 10a to verify that it's operating correctly? What data should you input in each program run?

- **11. (Program)**

  a. A senior salesperson is paid $800 a week, and a junior salesperson, $500 a week. Write a C++ program that accepts as input a salesperson's status in the character variable `status`. If `status` equals `s`, the senior salesperson's salary should be displayed; otherwise, the junior salesperson's salary should be displayed.

  b. How many runs should you make for the program written in Exercise 11a to verify that it's operating correctly? What data should you input in each program run?

- **12. (Program)**

  a. Write a C++ program that displays the message "I feel great today!" or "I feel down today #$#!" depending on the input. If the character `u` is entered in the variable `ch`, the first message should be displayed; otherwise, the second message should be displayed.

  b. How many runs should you make for the program written in Exercise 12a to verify that it's operating correctly? What data should you input in each program run?

- **13. (Program)**

  a. Write a program to display the following two prompts:

  Enter a month (use a 1 for Jan, etc.);
  Enter a day of the month:

  Have your program accept and store a number in the variable `month` in response to the first prompt and accept and store a number in the variable `day` in response to the second prompt. If the month entered isn't between 1 and 12, display a message informing the user that an invalid month has been entered. If the day entered isn't between 1 and 31, display a message informing the user that an invalid day has been entered.

  b. What will your program do if the user enters a number with a decimal point for the month? How can you make sure your if statements check for an integer number?

- **14. (Program)**

  a. Write, compile, and run a C++ program that accepts as input a character and determines whether the character is a lowercase letter. A lowercase letter is any character that's greater than or equal to `"a"` and less than or equal to `"z"`. If the entered character is a lowercase letter, display the message "The character just entered is a lowercase letter." If the entered letter isn't lowercase, display the message "The character just entered is not a lowercase letter."

  b. Modify the program written for Exercise 14a to also determine whether the entered character is an uppercase letter. An uppercase letter is any character greater than or equal to `"A"` and less than or equal to `"Z"`.

- **16. (Program)**

  Write, compile, and run a C++ program that asks the user to input two numbers. After your program accepts these numbers by using one or more `cin` object calls, have it check the numbers. If the first number entered is greater than the second number, the program should print the message "The first number is greater."; otherwise, it should print the message "The first number is not greater than the second." Test your program by entering the numbers 5 and 8 and then using the numbers 11 and 2. What will your program display if the two numbers entered are equal?

- **17. (Debug)**

  The following program displays the message Hello there! regardless of the letter input. Determine where the error is and why the program always causes the message to be displayed.

  ```cpp
  #include <iostream>
  using namespace std;
  int main()
  {
      char letter;

      cout << "Enter a letter: ";
      cin >> letter;
      if (letter = 'm')
          cout << "Hello there!" << endl;

      return 0;
  }
  ```

## 4.3 Nested if Statements

As you have seen, an if-else statement can contain any valid C++ simple or compound statements, including another if-else statement. Therefore, one or more if-else statements can be included in either part of an if-else statement. Including one or more if statements inside an existing if statement is called a nested if statement. For example, substituting the one-way if statement

```cpp
if (distance > 500)
    cout << "snap";
```

for `statement1` in this if statement

```cpp
if (hours < 9)
    statement1;
else
    cout << "pop";
```

results in the following nested if statement:

```cpp
if (hours < 9)
{
    if (distance > 500)
        cout << "snap";
}
else
    cout << "pop";
```

The braces around the inner one-way if statement are essential because in their absence, C++ associates an `else` with the closest unpaired `if`. Therefore, without the braces, the preceding statement is equivalent to the following:

```cpp
if (hours < 9)
    if (distance > 500)
        cout << "snap";
    else
        cout << "pop";
```

In this example, the `else` is paired with the inner `if`, which destroys the meaning of the original if-else statement. Notice also that the indentation is irrelevant, as far as the compiler is concerned. Whether the indentation exists or not, the statement is compiled by associating the last `else` with the closest unpaired `if`, unless braces are used to alter the default pairing. The process of nesting if statements can be extended indefinitely, so the `cout << "snap";` statement could be replaced by a complete if-else statement or another one-way if statement.

### The if-else Chain

In general, nesting in which one if-else statement is placed inside the if part of another if-else statement tends to be confusing and is best avoided in practice. However, an extremely useful construction is placing one if-else statement inside the else part of another if-else statement. Typically, this nesting is written in the following form:

```cpp
if (expression_1)
    statement1;
else if (expression_2)
    statement2;
else
    statement3;
```

This useful construction, called an if-else chain, is used extensively in programming applications. Each condition is evaluated in order, and if any condition is true, the corresponding statement is executed, and the remainder of the chain is terminated. The statement associated with the final `else` is executed only if no previous condition is satisfied. This final `else` serves as a default or catch-all case that's useful for detecting an impossible condition or an error condition.

- **2. (Program)**

  The grade level of undergraduate college students is typically determined according to the following schedule:

  | Number of Credits Completed | Grade Level |
  | --- | --- |
  | Less than 32 | Freshman |
  | 32 to 63 | Sophomore |
  | 64 to 95 | Junior |
  | 96 or more | Senior |

  Using this information, write a C++ program that accepts the number of credits a student has completed, determines the student's grade level, and displays the grade level.

- **3. (Program)**

  A student's letter grade is calculated according to the following schedule:

  | Numerical Grade | Letter Grade |
  | --- | --- |
  | Greater than or equal to 90 | A |
  | Less than 90 but greater than or equal to 80 | B |
  | Less than 80 but greater than or equal to 70 | C |
  | Less than 70 but greater than or equal to 60 | D |
  | Less than 60 | F |

  Using this information, write, compile, and run a C++ program that accepts a student's numerical grade, converts the numerical grade to an equivalent letter grade, and displays the letter grade.

- **4. (Program)**

  The interest rate paid on funds deposited in a bank is determined by the amount of time the money is left on deposit. For a particular bank, the following schedule is used:

  | Time on Deposit | Interest Rate |
  | --- | --- |
  | Greater than or equal to 5 years | .040 |
  | Less than 5 years but greater than or equal to 4 years | .035 |
  | Less than 4 years but greater than or equal to 3 years | .030 |
  | Less than 3 years but greater than or equal to 2 years | .025 |
  | Less than 2 years but greater than or equal to 1 year | .020 |
  | Less than 1 year | .015 |

  Write, compile, and run a C++ program that accepts the time funds are left on deposit and displays the interest rate corresponding with the time entered.

- **5. (Program)**

  Fluid flowing through a pipe can flow in a smooth, constant manner, called laminar flow; in a chaotic manner, called turbulent flow; or in an intermediate stage between smooth and turbulent flow, which is called transitional flow. In practice, a value known as the Reynolds number can be used to determine the type of flow. For a Reynolds number below 2000, the flow is laminar, and for a Reynolds number above 3000, the flow is turbulent. For a Reynolds number between 2000 and 3000, the flow is transitional.
