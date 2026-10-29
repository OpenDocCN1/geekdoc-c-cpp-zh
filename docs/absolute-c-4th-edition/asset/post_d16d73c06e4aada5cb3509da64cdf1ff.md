
# PROGRAMMING PROJECTS

1. A metric ton is 35,273.92 ounces. Write a program that will read the weight of a package of breakfast cereal in ounces and output the weight in metric tons as well as the number of boxes needed to yield one metric ton of cereal.

2. A government research lab has concluded that an artificial sweetener commonly used in diet soda will cause death in laboratory mice. A friend of yours is desperate to lose weight but cannot give up soda. Your friend wants to know how much diet soda it is possible to drink without dying as a result. Write a program to supply the answer. The input to the program is the amount of artificial sweetener needed to kill a mouse, the weight of the mouse, and the weight of the dieter. To ensure the safety of your friend, be sure the program requests the weight at which the dieter will stop dieting, rather than the dieter’s current weight. Assume that diet soda contains one-tenth of 1% artificial sweetener. Use a variable declaration with the modifier const to give a name to this fraction. You may want to express the percentage as the double value 0.001.

3. Workers at a particular company have won a 7.6% pay increase retroactive for six months. Write a program that takes an employee’s previous annual salary as input and outputs the amount of retroactive pay due the employee, the new annual salary, and the new monthly salary. Use a variable declaration with the modifier const to express the pay increase.

4. Negotiating a consumer loan is not always straightforward. One form of loan is the discount installment loan, which works as follows. Suppose a loan has a face value of $1,000. the interest rate is 15%, and the duration is 18 months. The interest is computed by multiplying the face value of $1,000 by 0.15, yielding $150. That figure is then multiplied by the loan period of 1.5 years to yield $225 as the total interest owed. That amount is immediately deducted from the face value, leaving the consumer with only $775. Repayment is made in equal monthly installments based on the face value. So the monthly loan payment will be $1,000 divided by 18, which is $55.56. This method of calculation may not be too bad if the consumer needs $775 dollars, but the calculation is a bit more complicated if the consumer needs $1,000. Write a program that will take three inputs: the amount the consumer needs to receive, the interest rate, and the duration of the loan in months. The program should then calculate the face value required in order for the consumer to receive the amount needed. It should also calculate the monthly payment.

5. Write a program that determines whether a meeting room is in violation of fire law regulations regarding the maximum room capacity. The program will read in the maximum room capacity and the number of people to attend the meeting. If the number of people is less than or equal to the maximum room capacity, the program announces that it is legal to hold the meeting and tells how many additional people may legally attend. If the number of people exceeds the maximum room capacity, the program announces that the meeting cannot be held as planned due to fire regulations and tells how many people must be excluded in order to meet the fire regulations.

6. An employee is paid at a rate of $16.78 per hour for regular hours worked in a week. Any hours over that are paid at the overtime rate of one and one-half times that. From the worker’s gross pay, 6% is withheld for Social Security tax, 14% is withheld for federal

# CHAPTER Flow of Control

- 2.1 BOOLEAN EXPRESSIONS 44
- Building Boolean Expressions 44
- Pitfall: Strings of Inequalities 45
- Evaluating Boolean Expressions 46
- Precedence Rules 48
- Pitfall: Integer Values Can Be Used as Boolean Values 52
- 
- 2.2 BRANCHING MECHANISMS 54
- if-else Statements 54
- Compound Statements 56
- Pitfall: Using = in Place of == 57
- Omitting the else 58
- Nested Statements 59
- Multiway if-else Statement 59
- The switch Statement 61
- Pitfall: Forgetting a break in a switch Statement 63
- Tip: Use switch Statements for Menus 63
- Enumeration Types 64
- The Conditional Operator 64
- 
- 2.3 LOOPS 66
- The while and do-while Statements 66
- Increment and Decrement Operators Revisited 69
- The Comma Operator 72
- The for Statement 73
- Tip: Repeat-N-Times Loops 76
- Pitfall: Extra Semicolon in a for Statement 76
- Pitfall: Infinite Loops 77
- The break and continue Statements 80
- Nested Loops 83
- 
- CHAPTER SUMMARY 83
- ANSWERS TO SELF-TEST EXERCISES 84
- PROGRAMMING PROJECTS 89

![](img/9505fd46e120aa9c1406715936ff6251_42_0.png)

# Flow of Control

> > “Would you tell me, please, which way I ought to go from here?”
> > “That depends a good deal on where you want to get to,” said the Cat.
> >
> > — Lewis Carroll, *Alice in Wonderland*

# INTRODUCTION

As in most programming languages, C++ handles flow of control with branching and looping statements. C++ branching and looping statements are similar to branching and looping statements in other languages. They are the same as in the C language and very similar to what they are in the Java programming language. Exception handling is also a way to handle flow of control. Exception handling is covered in Chapter 18.

## 2.1 Boolean Expressions

> > He who would distinguish the true from the false must have an adequate idea of what is true and false.
> >
> > — Benedict Spinoza, *Ethics*

Most branching statements are controlled by Boolean expressions. A **Boolean expression** is any expression that is either true or false. The simplest form for a Boolean expression consists of two expressions, such as numbers or variables, that are compared with one of the comparison operators shown in Display 2.1. Notice that some of the operators are spelled with two symbols, for example, ==, !=, <=, >=. Be sure to notice that you use a double equal sign for the equal sign and that you use the two symbols != for not equal. Such two-symbol operators should not have any space between the two symbols.

### BUILDING BOOLEAN EXPRESSIONS

You can combine two comparisons using the “and” operator, which is spelled && in C++. For example, the following Boolean expression is true provided x is greater than 2 and x is less than 7:

```
`(2 < x) && (x < 7)`
```

When two comparisons are connected using a &&, the entire expression is true, provided both of the comparisons are true; otherwise, the entire expression is false.

# THE "AND" OPERATOR, &&

You can form a more elaborate Boolean expression by combining two simpler Boolean expressions using the "and" operator, &&.

# SYNTAX FOR A BOOLEAN EXPRESSION USING &&

```
(Boolean_Exp_1) && (Boolean_Exp_2)
```

# EXAMPLE (WITHIN AN if-else STATEMENT)

```
if ( (score > 0) && (score < 10) )
    cout << "score is between 0 and 10.\n";
else
    cout << "score is not between 0 and 10.\n";
```

If the value of score is greater than 0 and the value of score is also less than 10, then the first cout statement will be executed; otherwise, the second cout statement will be executed. (if-else statements are covered a bit later in this chapter, but the meaning of this simple example should be intuitively clear.)

You can also combine two comparisons using the "or" operator, which is spelled || in C++. For example, the following is true provided y is less than 0 or y is greater than 12:

```
(y < 0) || (y > 12)
```

When two comparisons are connected using a ||, the entire expression is true provided that one or both of the comparisons are true; otherwise, the entire expression is false.

You can negate any Boolean expression using the ! operator. If you want to negate a Boolean expression, place the expression in parentheses and place the ! operator in front of it. For example, !(x < y) means "x is not less than y." The ! operator can usually be avoided. For example, !(x < y) is equivalent to x >= y. In some cases you can safely omit the parentheses, but the parentheses never do any harm. The exact details on omitting parentheses are given in the subsection entitled Precedence Rules.

# Pitfall

# STRINGS OF INEQUALITIES

Do not use a string of inequalities such as x < z < y. If you do, your program will probably compile and run, but it will undoubtedly give incorrect output. Instead, you must use two inequalities connected with an &&, as follows:

```
(x < z) && (z < y)
```
