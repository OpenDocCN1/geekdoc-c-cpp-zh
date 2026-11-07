
The first statement after the switch. In a switch, it’s good practice to test all possible values of the controlling expression. Also, providing a default case focuses you on the need to process exceptional conditions.

## Displaying the Grade Report

Lines 54–71 output a report based on the grades entered. Line 57 determines whether the user entered at least one grade. This helps us avoid dividing by zero, which for integer division causes the program to fail and for floating-point division produces the value nan (“not a number”). If so, line 59 calculates the average of the grades—recall that a double divided by an int produces a double result. Lines 62–67 then output the total of all the grades, the class average and the number of students who received each letter grade. If no grades were entered, line 70 outputs an appropriate message. The output in Fig. 4.6 shows a sample grade report based on 10 grades.

## switch Statement UML Activity Diagram

The following is the UML activity diagram for the general switch statement:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_222_0.png)

Most switch statements use a break in each case to terminate the switch after the case is processed. The diagram emphasizes this by including breaks and showing that the break at the end of a case causes control to exit the switch immediately. The break statement is not required for the switch’s last case or the optional default case when it appears last because execution continues with the next statement after the switch.

## Notes on cases

Each case in a switch statement must contain a constant integral expression—that is, any expression that evaluates to a constant integer value. You also can use enum constants (introduced in Section 5.9) and character literals—specific characters in single quotes, such as 'a', 'A' or '$', which represent the integer values of characters.⁷

In Chapter 10, OOP: Inheritance and Runtime Polymorphism, we present a more elegant way to implement switch logic. We use a technique called **polymorphism** to create programs that are often clearer, easier to maintain and extend than programs using switch logic.

## Checkpoint

- **1. (True/False)** Most switch statements do not use the break statement in each case.
  **Answer:** False. Most switch statements use a break in each case to terminate the switch after the case is processed.
- **2. (True/False)** Providing a default case in a switch focuses you on the need to process exceptional conditions.
  **Answer:** True.
- **3. (What’s Wrong with This Code?)** Find the error in the following code and explain how to correct it.

```cpp
switch (n) {
    case 1:
        cout << "The number is 1\n";
    case 2:
        cout << "The number is 2\n";
        break;
    default:
        cout << "The number is not 1 or 2\n";
        break;
}
```

**Answer:** The code is missing a break statement in the first case. So, if the value of n is 1, the output statements in cases 1 and 2 will both execute. To fix this, add a break statement after the output statement in the first case.

## 4.9 Selection Statements with Initializers

Earlier, we introduced the for iteration statement. In the for header’s initialization section, we declared and initialized a control variable, which limited that variable’s scope to the for statement. Selection statements with initializers enable you to include variable initializers before the condition in an if or if...else statement and before the controlling expression of a switch statement. As with the for statement, these variables are known only in the statements where they’re declared. Figure 4.7 shows if...else statements with initializers (lines 8–13 and 15–20). We’ll use both if...else and switch statements with initializers in Fig. 5.5, which implements a popular casino dice game.

```cpp
// fig04_07.cpp
// if statements with initializers.
#include <format>
#include <iostream>
using namespace std;

int main() {
    if (int value{7}; value == 7) {
        cout << format("value is {}\n", value);
    }
    else {
        cout << format("value is not 7; it is {}\n", value);
    }

    if (int value{13}; value == 9) {
        cout << format("value is {}\n", value);
    }
    else {
        cout << format("value is not 9; it is {}\n", value);
    }
}
```

```text
value is 7
value is not 9; it is 13
```

**Fig. 4.7** | `if` statements with initializers.

### Syntax of Selection Statements with Initializers

For an `if` or `if...else` statement, you place the initializer first in the condition’s parentheses. For a `switch` statement, you place the initializer first in the controlling expression’s parentheses. The initializer must end with a semicolon (`;`), as in lines 8 and 15. The initializer can declare multiple variables of the same type in a comma-separated list.

### Scope of Variables Declared in the Initializer

Any variable declared in the initializer of an `if`, `if...else` or `switch` statement may be used throughout the remainder of the statement. In lines 8–13, we use the variable `value` to determine which branch of the `if...else` statement to execute, then use `value` in the output statements of both branches. When the `if...else` statement terminates, `value` no longer exists, so we can use that identifier again in the second `if...else` statement to declare a new variable known only in that statement.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_224_0.png)

## Checkpoint

- **1. (True/False)** The scope of a variable declared in the initializer of an `if`, `if...else` or `switch` statement is the remainder of the block in which that statement is defined.
  **Answer:** False. The scope of such a variable is the remainder of that `if`, `if...else` or `switch` statement.

## 4.10 break and continue Statements

In addition to selection and iteration statements, C++ provides break and continue statements to alter the flow of control. The preceding section showed how break could be used to terminate a switch statement’s execution. This section discusses how to use break in iteration statements.

### break Statement

Executing a break statement in a while, for, do…while or switch causes immediate exit from that statement—execution continues with the first statement after the control statement. Common uses of break include escaping early from a loop or exiting a switch (as in Fig. 4.6). Figure 4.8 demonstrates a break statement exiting early from a for statement.

```cpp
1  // fig04_08.cpp
2  // break statement exiting a for statement.
3  #include <iostream>
4  using namespace std;
5
6  int main() {
7      int count; // control variable also used after loop
8
9      for (count = 1; count <= 10; ++count) { // loop 10 times
10         if (count == 5) {
11             break; // terminates for loop if count is 5
12         }
13
14         cout << count << " ";
15     }
16
17     cout << "\nBroke out of loop at count = " << count << "\n";
18  }
```

```text
1 2 3 4
Broke out of loop at count = 5
```

**Fig. 4.8** | `break` statement exiting a `for` statement.

When the if statement nested at lines 10–12 in the for statement (lines 9–15) detects that count is 5, the break statement at line 11 executes. This terminates the for statement, and the program proceeds to line 17 (immediately after the for statement), which displays a message indicating the control variable’s value when the loop terminated. The loop fully executes its body only four times instead of 10. Note that we could have initialized count in line 7 and left the for header’s initialization section empty, as in:

```cpp
for ( ; count <= 10; ++count) { // loop 10 times
```

### continue Statement

Executing the continue statement in a while, for or do…while skips the remaining statements in the loop body and proceeds with the next iteration of the loop. In while and do…while statements, the program evaluates the loop-continuation test immediately after
