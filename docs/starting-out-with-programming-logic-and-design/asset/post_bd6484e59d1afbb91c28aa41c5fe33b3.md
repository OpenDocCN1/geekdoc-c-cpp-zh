
## 4.2 Dual Alternative Decision Structures

**CONCEPT:** A dual alternative decision structure will execute one group of statements if its Boolean expression is true, or another group if its Boolean expression is false.

A dual alternative decision structure has two possible paths of execution—one path taken if a condition is true, and the other path taken if the condition is false. Figure 4-8 shows a flowchart for a dual alternative decision structure.

Figure 4-8 A dual alternative decision structure

![](img/c939132f78787c7f339c6977b3fc8c85_157_0.png)

The decision structure in the flowchart tests the condition `temperature < 40`. If this condition is true, the statement `Display "A little cold, isn't it?"` is performed. If the condition is false, the statement `Display "Nice weather we're having."` is performed.

In pseudocode we write a dual alternative decision structure as an If-Then-Else statement. Here is the general format of the If-Then-Else statement:

```
If condition Then
    statement
    statement
    etc.    These statements are executed if the condition is true.
Else
    statement
    statement
    etc.    These statements are executed if the condition is false.
End If
```

In the general format, the condition is any Boolean expression. If the expression is true, the statements that appear next are executed, up to the line that reads Else. If the expression is false, the statements that appear between Else and End are executed. The line that reads End marks the end of the If-Then-Else statement.

## Chapter 4 Decision Structures and Boolean Logic

The following pseudocode shows an example of an If-Then-Else statement. The pseudocode matches the flowchart that was shown in Figure 4-8.

```
If temperature < 40 Then
    Display "A little cold, isn't it?"
Else
    Display "Nice weather we're having."
End If
```

We will refer to the line that reads Else as the Else clause. When you write an If-Then-Else statement, use the following style conventions:

- Make sure the If clause, the Else clause, and the End If clause are aligned.
- Indent the conditionally executed statements that appear between the If clause and the Else clause, and between the Else clause and the End If clause.

This is shown in Figure 4-9.

Figure 4-9 Programming style with an If-Then-Else statement

![](img/c939132f78787c7f339c6977b3fc8c85_158_0.png)

## In the Spotlight:

### Using the If-Then-Else Statement

Chris owns an auto repair business and has several employees. If an employee works over 40 hours in week, Chris pays 1.5 times his regular hourly rate for over 40 hours. Chris has asked you to design a simple payroll program that calculates an employee's gross pay, including any overtime wages. You design the following algorithm:

- Get the number of hours worked.
- Get the hourly pay rate.
- If the employee worked more than 40 hours, calculate the gross pay with overtime. Otherwise, calculate the gross pay as usual.
- Display the gross pay.

You go through the top-down design process and create the hierarchy chart shown in Figure 4-10. As shown in the hierarchy chart, the main module will call four other modules.

- hoursWorked—This module will ask the user to enter the number of hours worked.
- getPayRate—This module will ask the user to enter the pay rate.
- calcPayWithOvertime—This module will calculate an employee's pay with overtime.
- calcRegular—This module will calculate the gross pay for an employee with no overtime.

## 4.2 Dual Alternative Decision Structures

The main module, which executes when the program is run, will call these modules and then display the gross pay. The pseudocode for the program is shown in Program 4-2. Figures 4-11 and 4-12 show flowcharts for each of the modules.

## Figure 4-10 Hierarchy chart

![](img/c939132f78787c7f339c6977b3fc8c85_159_0.png)

## Program 4-2

```
// Global constants
Constant Integer BASE_HOURS = 40
Constant OT MULTIPLIER = 1.5

Module main()
  // Local variables
  Declare Real hoursWorked,payRate, grossPay

  // Get the number of hours worked.
  Call getHoursWorked(hoursWorked)
  // Get the hourly pay rate.
  Call getPayRate(payRate)

  // Calculate the gross pay.
  If hoursWorked > BASE_HOURS Then
    Call calcPayWithOT(hoursWorked,payRate,
      grossPay)
  Else
    Call calcRegularPay(hoursWorked,payRate,
      grossPay)
  End If

  // Display the gross pay.
  Display "The gross pay is $",grossPay
  End Module

// The getHoursWorked module gets the number
// of hours worked and stores it in the
// 30 // hours parameter.
Module getHoursWorked(Real hours)
    Display "Enter the number of hours worked."
    Input hours
End Module

// The getPayRate module gets the hourly
// pay rate and stores it in the
// rate parameter.
Module getPayRate(Real rate)
    Display "Enter the pay rate."
    Input rate
End Module
```

## Chapter 4 Decision Structures and Boolean Logic

## Figure 4-12 Flowcharts for the other modules

![](img/c939132f78787c7f339c6977b3fc8c85_162_0.png)

Checkpoint

- 4.8 How does a dual alternative decision structure work?
- 4.9 What statement do you use in pseudocode to write a dual alternative decision structure?
- 4.10 When you write an If-Then-Else statement, under what circumstances do the statements between Else and End execute?

## 4.3 Comparing Strings

**CONCEPT:** Most programming languages allow you to compare strings. This allows you to create decision structures that test the value of a string.

You saw in the preceding examples how numbers can be compared. Most programming languages also allow you to compare strings. For example, look at the following pseudocode:

```
Declare String name1 = "Mary"
Declare String name2 = "Mark"
If name1 == name2 Then
    Display "The names are the same."
Else
    Display "The names are NOT the same."
End If
```

The == operator tests name1 and name2 to determine whether they are equal. Because the strings "Mary" and "Mark" are not equal, the Else will display the message "The names are not the."

You can compare String variables with string literals as well. Assume month is a String variable. The following pseudocode uses the != operator to determine whether month is not equal to "October".

```
If month != "October" Then
    statement
End If
```

The pseudocode in Program 4-3 demonstrates how two strings can be compared. The program prompts the user to enter a password and then determines whether the string entered is equal to "prospero".

| Program 4-3 |
| :--- |

```
// A variable to hold a password.
Declare String password

// Prompt the user to enter the password.
Display "Enter the password."
Input password

// Determine whether the correct password
// was entered.
If password == "prospero" Then
    Display "Password accepted."
Else
    Display "Sorry, that is not the correct password."
End If
```
