
```
add value of x with y and store the result in z
set the value of flag (of type bool) to false
```

**PR-30.** Find any error in each of the following statements (x, y, z, and t are numeric types).

```cpp
x += 7;
y *= y;
z + 6 = z;
3t = 12;
```

**PR-31.** Find any error in each of the following statements (assuming that all variables are numeric types).

```cpp
x = 7 = 4;
y *= y = 6;
z = z + 5 = 8;
hello = 12;
```

**PR-32.** Assume x is of type bool, y is of type char, z is of type short, and t is of type float. What implicit promotion takes place in each of the following expressions, and what is the value of each expression?

```
x + 4
y * 2
z - 24;
t + 23.4;
```

**PR-33.** Assume x is of type int, y is of type long, z is of type long long, and t is of type long double. What implicit promotion takes place in each of the following expressions?

```
x + y
y * z
z - t;
```

**PR-34.** What will be output from the following program segment?

```cpp
double x = -909.245;
cout << fixed << setprecision (2) << x << endl;
cout << fixed << setw (15) << setprecision (3) << setfill ('*') << x;
```

**PR-35.** What will be output from the following program segment?

```cpp
int x = 50;
cout << setw(10) << setfill ('*') << x;
```

**PR-36.** What will be output from the following program segment?

```cpp
int n1 = 10, n2 = 20;
char ch = '#';
cout << setw(n1) << setfill (ch) << 241 << endl;
cout << setw(n2) << setfill (ch) << 14672;
```

**PR-37.** What will be output from the following program segment?

```cpp
int n1 = 8, n2 = 12;
char ch = '#';
cout << setw(n1) << setprecision (3) << setfill (ch) << 475.12 << endl;
cout << setw(n2) << setprecision (4) << setfill (ch) << 0.151;
```

**PR-38.** What will be output when the following code is executed and we enter the Boolean value false?

```cpp
bool x;
cin >> boolalpha >> x;
cout << x;
```

**PR-39.** What will be output when the following code is run and we input 72?

```cpp
int x;
cin >> oct >> x;
cout << x;
```

**PR-40.** What will be output when the following code is run and we input 72?

```cpp
int x;
cin >> hex >> x;
cout << x;
```

### Programs

- **PRG-1.** Write a program that finds the maximum and minimum values for a **short** and **unsigned int** in your computer.
- **PRG-2.** Write a program that finds the minimum and maximum values for a **long**, and a **long long** in your computer.
- **PRG-3.** Write a program that finds the minimum and maximum values for a **float** and a **double** in your computer.
- **PRG-4.** Write a program that extracts and prints the second digit of an input data of type **int**.
- **PRG-5.** Write a program that individually extracts the rightmost three digits of an input data of type **int**.
- **PRG-6.** Write a program that, given a three-digit integer, constructs and prints another integer whose digits are in the reverse order of the given one. For example, given 372, the program prints 273.
- **PRG-7.** Write a program that, given a number of hours, calculates the number of weeks, days, and hours included in that number.
- **PRG-8.** Write a program that, given the time duration of a task in the number of hours, minutes, and seconds, calculates duration in seconds.
- **PRG-9.** Write a program that inputs the number of seconds (a long value) and changes it to days, hours, minutes, and seconds.
- **PRG-10.** Write a program that inputs four scores (int values) and finds and prints the average of the scores (a double value).
- **PRG-11.** Write a program that helps a cashier at a store find the amount of change given, the amount of a purchase in dollars and cents, and the amount of dollars and cents given by the customer. The answer should be in dollars, quarters, dimes, nickels, and pennies.
- **PRG-12.** Write a program that, given a temperature in Celsius, calculates and prints the temperature in Fahrenheit using the formula F = (9/5) C + 32.
- **PRG-13.** Write a program that, given a temperature in Fahrenheit, calculates and prints the temperature in Centigrade using the formula C = (F − 32) * 5/9.
- **PRG-14.** Assume a party of three couples dines in a restaurant. The first family has two children. Each of the other families has one child. Write a program that divides the bill among each family if a child is charged 3/4 of an adult share. The total charge (before tax) is given as an input. The tax is 9.5 percent, and 20 percent must be added for service.
- **PRG-15.** An hourly employee is paid regular pay per hour for 40 hours a week. She will be paid 60 percent more for every hour she works over 40 hours. Write a program that asks an employee to enter the number of extra hours worked last week and the weekly rate and then calculates and prints total payment.
- **PRG-16.** Write a program to create a customer's bill for a company. The company sells only three products: TV sets, DVD players, and remote controllers. The unit prices are $1400.00, $220.00, and $35.20, respectively. The program must read from the keyboard the quantity of each piece of equipment purchased. It then calculates the cost of each item, the subtotal, and the total cost after an 8.25 percent sales tax.

## 4 Selection

The programs we wrote in previous chapters were based on a sequential execution of statements. The programs were mostly made of input statements, calculation statements, and output statements. Every time we ran the program, all statements in the program were executed one after another. The sequential execution of statements may solve simple problems, but we also need to have control statements. In this chapter, we discuss the first group of control statements: selection statements. A selection statement allows the programmer to choose between different actions based on one or more conditions.

**Objectives**

After you have read and studied this chapter, you should be able to:

- Discuss the need for relational and equality expressions in achieving simple selections.
- Understand how we can make a one-way selection using the *if* statement.
- Understand how we can make a two-way selection using the *if-else* statement.
- Understand how we can make a multiway selection using the nested *if-else* statement.
- Show how complex decisions can be made by combining relational/equality expressions with logical expressions.
- Understand how we can make a multiway selection in which the decision is based on discrete values using a *switch* statement.
- Show how we can use a *conditional expression* instead of a simple *if-else* statement.

### 4.1 SIMPLE SELECTION

To solve some problems, we must make decisions based on the test of a *true-false* condition. If the condition is true, we need to execute a set of statements; if the condition is false, we need to execute another set of statements (or no statements). This process is referred to as selection. The question is, How do we create the condition that should be tested? The answer is that we use expressions whose values are either *true* or *false*.

#### 4.1.1 Relational and Equality Expressions

To make simple decisions, we need either relational or equality expressions. These expressions are shown in Appendix C, but we show them in Table 4.1 for quick reference. We distinguish between the two groups because they occupy different levels of precedence (11 and 10).

**Table 4.1** Relational and equality expressions

| Group | Name | Operator | Expression | Pred | Assoc |
| --- | --- | --- | --- | --- | --- |
| Relational | less | < | expr < expr | 11 | → |
|  | less or equal | <= | expr <= expr |  |  |
|  | greater | > | expr > expr |  |  |
|  | greater or equal | >= | expr >= expr |  |  |
| Equality | equal | == | expr == expr | 10 | → |
|  | not equal | != | expr != expr |  |  |

#### Relational Expressions

As Table 4.1 shows, **relational expressions** use four relational operators to compare two values. Note that the result of (a <= b) is *true* if a is equal to or if a is less than b; it is *false* if a is greater than b. Similarly, the result of (a >= b) is *true* if a is greater than or equal to b; the result is *false* if a is less than b. The type of the left and the right expression must be the same when the comparison is evaluated. If the two expressions are not the same type, the conversion we discussed in Chapter 3 is applied. The following shows some examples of relational operators.

```cpp
3 < 4              // The result is true because 3 is less than 4.
12.78 < 7.36       // The result is false because 12.78 is not less than 7.36.
5 <= 3.24          // The left operand is first promoted to 5.0. The result is false.
5.0 <= 5           // The right operand is first promoted to 5.0. The result is true.
3 > false          // The right operand is promoted to 0. The result is true.
5 >= 2.2           // The left operand is promoted to 5.0. The result is true.
```

#### Equality Expressions

Table 4.1 also shows two **equality expressions** that determine if two entities are equal or not. Note that the result of (a == b) is *true* if a is equal to b; it is *false* if a is not equal to b. Similarly, the result of (a != b) is *true* if the value of a is different from the value of b; the result is false if they are equal. The type of the left and the right expressions must be the same when the comparison is evaluated. If the two expressions are not the same type, the conversion we discussed in Chapter 3 is applied. The following shows some equality expressions and their results.

```cpp
3 == 4             // The result is false.
true == false      // The expression is converted to (1 == 0). The result is false.
true != false      // The expression is converted to (1 != 0). The result is true.
3 != false         // The right operand is changed to 0. The result is true.
65 != 'A'          // The result is false because 'A' is converted to 65.
```
