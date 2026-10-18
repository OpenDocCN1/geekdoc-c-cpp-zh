
Display 2.6 illustrates how `/` and `%` work with values of type `int`.

**DISPLAY 2.6 Integer Division**

When used with negative values of type `int`, the result of the operators `/` and `%` can be different for different implementations of C++. Thus, you should use `/` and `%` with `int` values only when you know that both values are non-negative.

Any reasonable spacing will do in arithmetic expressions. You can insert spaces before and after operators and parentheses, or you can omit them. Do whatever produces a result that is easy to read.

You can specify the order of operations by inserting parentheses, as illustrated in the following two expressions:

```
(x + y) * z
x + (y * z)
```

To evaluate the first expression, the computer first adds `x` and `y` and then multiplies the result by `z`. To evaluate the second expression, it multiplies `y` and `z` and then adds the result to `x`. Although you may be used to using mathematical formulas that contain square brackets and various other forms of parentheses, that is not allowed in C++. C++ allows only one kind of parentheses in arithmetic expressions. The other varieties are reserved for other purposes.

If you omit parentheses, the computer will follow rules called precedence rules that determine the order in which the operators, such as `+` and `*`, are performed. These precedence rules are similar to rules used in algebra and other mathematics classes. For example,

```
x + y * z
```

is evaluated by first doing the multiplication and then the addition. Except in some standard cases, such as a string of additions or a simple multiplication embedded inside an addition, it is usually best to include the parentheses, even if the intended order of operations is the one dictated by the precedence rules. The parentheses make the expression easier to read and less prone to programmer error. A complete set of C++ precedence rules is given in Appendix 2.

Display 2.7 shows some examples of common kinds of arithmetic expressions and how they are expressed in C++.

## SELF-TEST EXERCISES

- 15. Convert each of the following mathematical formulas to a C++ expression:  
  3x    3x + y    (x + y)/7    (3x + y)/(z + 2)

- 16. What is the output of the following program lines when embedded in a correct program that declares all variables to be of type `char`?

```
a = 'b';
b = 'c';
c = a;
cout << a << b << c << 'c';
```

- 17. What is the output of the following program lines when embedded in a correct program that declares `number` to be of type `int`?

```
number = (1/3) * 3;
cout << "(1/3) * 3 is equal to " << number;
```

- 18. Write a complete C++ program that reads two whole numbers into two variables of type `int` and then outputs both the whole-number part and the remainder when the first number is divided by the second. This can be done using the operators `/` and `%`.

- 19. Given the following fragment that purports to convert from degrees Celsius to degrees Fahrenheit, answer the following questions:

```
double c = 20;
double f;
f = (9/5) * c + 32.0;
```

- a. What value is assigned to `f`?
- b. Explain what is actually happening, and what the programmer likely wanted.
- c. Rewrite the code as the programmer intended.

- 20. What is the output of the following program lines when embedded in a correct program that declares `month`, `day`, `year`, and `date` to be of type `string`?

```
month = "03";
day = "04";
year = "06";
date = month + day + year;
cout << date << endl;
```

## More Assignment Statements

There is a shorthand notation that combines the assignment operator (`=`) and an arithmetic operator so that a given variable can have its value changed by adding, subtracting, multiplying by, or dividing by a specified value. The general form is

```
Variable Op = Expression
```

which is equivalent to

```
Variable = Variable Op (Expression)
```

`Op` is an operator such as `+`, `-`, `*`, or `/`. The `Expression` can be another variable, a constant, or a more complicated arithmetic expression. Following are examples:

| Example | Equivalent to: |
|---|---|
| `count += 2;` | `count = count + 2;` |
| `total -= discount;` | `total = total - discount;` |
| `bonus *= 2;` | `bonus = bonus * 2;` |
| `time /= rushFactor;` | `time = time / rushFactor;` |
| `change %= 100;` | `change = change % 100;` |
| `amount *= cnt1 + cnt2;` | `amount = amount * (cnt1 + cnt2);` |

## 2.4 SIMPLE FLOW OF CONTROL

> "If you think we're wax-works," he said, "you ought to pay, you know. Wax-works weren't made to be looked at for nothing. Nohow!"
> 
> "Contrariwise," added the one marked "DEE," "if you think we're alive, you ought to speak."
> 
> LEWIS CARROLL, Through the Looking-Glass

The programs you have seen thus far each consist of a simple list of statements to be executed in the order given. However, to write more sophisticated programs, you will also need some way to vary the order in which statements are executed. The order in which statements are executed is often referred to as flow of control. In this section we will present two simple ways to add some flow of control to your programs. We will discuss a branching mechanism that lets your program choose between two alternative actions, choosing one or the other depending on the values of variables. We will also present a looping mechanism that lets your program repeat an action a number of times.

### A Simple Branching Mechanism

Sometimes it is necessary to have a program choose one of two alternatives, depending on the input. For example, suppose you want to design a program to compute a week's salary for an hourly employee. Assume the firm pays an overtime rate of one-and-one-half times the regular rate for all hours after the first 40 hours worked. As long as the employee works 40 or more hours, the pay is then equal to

```
rate * 40 + 1.5 * rate * (hours - 40)
```

However, if there is a possibility that the employee will work less than 40 hours, this formula will unfairly pay a negative amount of overtime. (To see this, just substitute 10 for `hours`, 1 for `rate`, and do the arithmetic. The poor employee will get a negative paycheck.) The correct pay formula for an employee who works less than 40 hours is simply

```
rate * hours
```

If both more than 40 hours and less than 40 hours of work are possible, then the program will need to choose between the two formulas. In order to compute the employee's pay, the program action should be

Decide whether or not `(hours > 40)` is true.

If it is, do the following assignment statement:

```
grossPay = rate * 40 + 1.5 * rate * (hours - 40);
```

If it is not, do the following:

```
grossPay = rate * hours;
```

There is a C++ statement that does exactly this kind of branching action. The `if-else` statement chooses between two alternative actions. For example, the wage calculation we have been discussing can be accomplished with the following C++ statement:

```
if (hours > 40)
    grossPay = rate * 40 + 1.5 * rate * (hours - 40);
else grossPay = rate * hours;
```

A complete program that uses this statement is given in Display 2.8.

Two forms of an `if-else` statement are described in Display 2.9. The first is the simple form of an `if-else` statement; the second form will be discussed in the subsection entitled "Compound Statements." In the first form shown, the two statements may be any executable statements. The `Boolean_Expression` is a test that can be checked to see if it is true or false, that is, to see if it is satisfied or not. For example, the `Boolean_Expression` in the earlier `if-else` statement is

```
hours > 40
```

When the program reaches the `if-else` statement, exactly one of the two embedded statements is executed. If the `Boolean_Expression` is true (that is, if it is satisfied), then the `Yes_Statement` is executed; if the `Boolean_Expression` is false (that is, if it is not satisfied), then the `No_Statement` is executed. Notice that the `Boolean_Expression` must be enclosed in parentheses. (This is required by the syntax rules for `if-else` statements in C++.) Also notice that an `if-else` statement has two smaller statements embedded in it.

**DISPLAY 2.8 An if-else Statement (part 1 of 2)**

```
1   #include <iostream>
2   using namespace std;
3   int main()
4   {
5       int hours;
6       double grossPay, rate;
7       cout << "Enter the hourly rate of pay: $";
8       cin >> rate;
9       cout << "Enter the number of hours worked,\n"
10      << "rounded to a whole number of hours: ";
11      cin >> hours;
12      if (hours > 40)
13      grossPay = rate * 40 + 1.5 * rate * (hours - 40);
14      else
15      grossPay = rate * hours;
16      cout.setf(ios::fixed);
17      cout.setf(ios::showpoint);
18      cout.precision(2);
19      cout << "Hours = " << hours << endl;
20      cout << "Hourly pay rate = $" << rate << endl;
21      cout << "Gross pay = $" << grossPay << endl;
22      return 0;
23  }
```

**Sample Dialogue 1**

```
Enter the hourly rate of pay: $20.00
Enter the number of hours worked,
rounded to a whole number of hours: 30
Hours = 30
Hourly pay rate = $20.00
Gross pay = $600.00
```
