
## Figure 5.1 if flowchart

![](img/e84ad11adb18201d71595b31ce6c9eff_101_0.png)

- The Boolean expression condition determines whether or not the body will be executed. The Boolean expression must be enclosed within parentheses as shown.

- The statement is the statement to be executed if the Boolean expression is true. The statement makes up the body of the if statement. Section 5.4 shows how the body can be composed of multiple statements.

Good coding style dictates we should indent the body to emphasize the optional execution and improve the program's readability. The compiler does not require the indentation. Sometimes programmers will place a one-statement body on the same line as the if; for example, the following if statement optionally assigns y:

```cpp
if (x < 10)
    y = x;
```

and could be written as

```cpp
if (x < 10) y = x;
```

but should not be written as

```cpp
if (x < 10)
    y = x;
```

because the lack of indentation hides the fact that the program optionally executes the assignment statement. The compiler will accept it, but it is misleading to human readers accustomed to the indentation convention. The compiler, of course, will accept the code written as

```cpp
if (x<10) y=x;
```

but the lack of spaces makes it difficult for humans to read.

![](img/e84ad11adb18201d71595b31ce6c9eff_102_0.png)

When the if statement is written the preferred way using two lines of source code, it is important not to put a semicolon at the end of the first line:

```cpp
if (x < 10); // No! Don't do this!
    y = x;
```

Here, the semicolon terminates the if statement, but the indentation implies that the second line is intended to be the body of the if statement. The compiler, however, interprets the badly formatted if statement as if it were written as

```cpp
if (x < 10)
    ; // This is what is really going on.
    y = x;
```

This is legal in C++; it means the if statement has an empty body. In which case the assignment is not part of the body. The assignment statement is after the body and always will be executed regardless of the truth value of the Boolean expression.

When checking for equality, as in
if (x == 10)
std::cout << "ten";
be sure to use the relational equality operator (==), not the assignment operator (=). Since an assignment statement has a value (the value that is assigned, see Section 4.3), C++ allows = within the conditional expression. It is, however, almost always a mistake when beginning programmers use = in this context. Visual C++ at warning Level 4 checks for the use of assignment within a conditional expression; the default Level 3 does not.

## 5.4 Compound Statements

Sometimes you need to optionally execute more than one statement based on a particular condition. Listing 5.4 (alternatedivision.cpp) shows how you must use curly braces to group multiple statements together into one compound statement.

### Listing 5.4: alternatedivision.cpp

```cpp
#include <iostream>
int main() {
  int dividend, divisor, quotient;
  // Get two integers from the user
  std::cout << "Please enter two integers to divide:";
  std::cin >> dividend >> divisor;
  // If possible, divide them and report the result
  if (divisor != 0) {
    quotient = dividend / divisor;
    std::cout << dividend << " divided by " << divisor << " is "
              << quotient << '\n';
  }
}
```

The assignment statement and printing statement are both a part of the body of the if statement. Given the truth value of the Boolean expression divisor != 0 during a particular program run, either both statements will be executed or neither statement will be executed.

A compound statement consists of zero or more statements grouped within curly braces. We say the curly braces define a block of statements. As a matter of style many programmers always use curly braces to delimit the body of an if statement even if the body contains only one statement.

```cpp
if (x < 10) {
  y = x;
}
```

They do this because it is easy to introduce a logic error if additional statements are added to the body later and the programmer forgets to add the required curly braces.

The format of the following code

```cpp
if (x < 10)
    y = x;
    z = x + 5;
```

implies that both assignments are part of the body of the if statement. Since multiple statements making up the body must be in a compound statement within curly braces, the compiler interprets the code fragment as if it had been written

![](img/e84ad11adb18201d71595b31ce6c9eff_104_0.png)

```cpp
if (x < 10)
    y = x;
    z = y + 5;
```

Such code will optionally execute the first assignment statement and *always* execute the second assignment statement.

The programmer probably meant to write it as

```cpp
if (x < 10) {
    y = x;
    z = x + 5;
}
```

The curly braces are optional if the body consists of a single statement. If the body consists of only one statement and curly braces are not used, then the semicolon that terminates the statement in the body also terminates the if statement. If curly braces are used to delimit the body, a semicolon is not required after the body's close curly brace.

An empty pair of curly braces represents an empty block. An empty block is a valid compound statement.

## 5.5 The if/else Statement

One undesirable aspect of Listing 5.3 (betterdivision.cpp) is if the user enters a zero divisor, the program prints nothing. It may be better to provide some feedback to the user to indicate that the divisor provided cannot be used. The if statement has an optional else clause that is executed only if the Boolean expression is false. Listing 5.5 (betterfeedback.cpp) uses the if/else statement to provide the desired effect.

### Listing 5.5: betterfeedback.cpp

```cpp
#include <iostream>

int main() {
    int dividend, divisor;

    // Get two integers from the user
    std::cout << "Please enter two integers to divide:";
    std::cin >> dividend >> divisor;

    // If possible, divide them and report the result
```

## Figure 5.2 if/else flowchart

![](img/e84ad11adb18201d71595b31ce6c9eff_105_0.png)

```cpp
if (divisor != 0)
    std::cout << dividend << "/" << divisor << " = "
              << dividend/divisor << '\n';
else
    std::cout << "Division by zero is not allowed\n";
}
```

A given program run will execute exactly one of either the `if` body or the `else` body. Unlike in Listing 5.3 (betterdivision.cpp), a message is always displayed.

```
Please enter two integers to divide: 32 0
Division by zero is not allowed
```

The `else` clause contains an alternate body that is executed if the condition is false. The program's flow of execution is shown in Figure 5.2.

Listing 5.5 (betterfeedback.cpp) avoids the division by zero run-time error that causes the program to terminate prematurely, but it still alerts the user that there is a problem. Another application may handle the situation in a different way; for example, it may substitute some default value for `divisor` instead of zero.

The general form of an `if`/`else` statement is

![](img/e84ad11adb18201d71595b31ce6c9eff_106_0.png)

- The reserved word if begins the if/else statement.
- The condition is a Boolean expression that determines whether the running program will execute statement 1 or statement 2. As with the simple if statement, the condition must appear within parentheses.
- The program executes statement 1 if the condition is true. To make the if/else statement more readable, indent statement 1 more spaces than the if line. This part of the if statement is sometimes called the body of the if.
- The reserved word else begins the second part of the if/else statement.
- The program executes statement 2 if the condition is false. To make the if/else statement more readable, indent statement 2 more spaces than the else line. This part of the if/else statement is sometimes called the body of the else.

The body of the else clause of an if/else statement may be a compound statement:

```cpp
if (x == y)
    std::cout << x;
else {
    x = 0;
    std::cout << y;
}
```

or the if body alone may be a compound statement:

```cpp
if (x == y) {
    std::cout << x;
    x = 0;
}
else
    std::cout << y;
```

or both parts may be compound:

```cpp
if (x == y) {
    std::cout << x;
    x = 0;
}
```
