
## DISPLAY 2.8 An if-else Statement (part 2 of 2)

### Sample Dialogue 2

```
Enter the hourly rate of pay: $10.00
Enter the number of hours worked,
rounded to a whole number of hours: 41
Hours = 41
Hourly pay rate = $10.00
Gross pay = $415.00
```

## DISPLAY 2.9 Syntax for an if-else Statement

### A Single Statement for Each Alternative:

```
1   if (Boolean_Expression)
2       Yes_Statement
3   else
4       No_Statement
```

### A Sequence of Statements for Each Alternative:

```
5   if (Boolean_Expression)
6   {
7       Yes_Statement_1
8       Yes_Statement_2
9       ...
10      Yes_Statement_Last
11  }
12  else
13  {
14      No_Statement_1
15      No_Statement_2
16      ...
17      No_Statement_Last
18  }
```

A Boolean expression is any expression that is either true or false. An if-else statement always contains a Boolean_Expression. The simplest form for a Boolean_Expression consists of two expressions, such as numbers or variables, that are compared with one of the comparison operators shown in Display 2.10. Notice that some of the operators are spelled with two symbols: for example, ==, !=, <=, >=. Be sure to notice that you use a double equal == for the equal sign, and

The inner parentheses around the comparisons are not required, but they do make the meaning clearer, and we will normally include them.

You can negate any Boolean expression using the ! operator. If you want to negate a Boolean expression, place the expression in parentheses and place the ! operator in front of it. For example, !(x < y) means “x is not less than y.”

## The "and" Operator &&

You can form a more elaborate Boolean expression by combining two simple tests using the "and" operator &&.

### SYNTAX (FOR A BOOLEAN EXPRESSION USING &&)

```
(Comparison_1) && (Comparison_2)
```

### EXAMPLE (WITHIN AN if-else STATEMENT)

```
if ( (score > 0) && (score < 10) )
    cout << "score is between 0 and 10\n";
else
    cout << "score is not between 0 and 10.\n";
```

If the value of score is greater than 0 and the value of score is also less than 10, then the first cout statement will be executed; otherwise, the second cout statement will be executed.

Since the Boolean expression in an if-else statement must be enclosed in parentheses, you should place a second pair of parentheses around the negated expression when it is used in an if-else statement. For example, an if-else statement might begin as follows:

```
if (!(x < y))
    ...
```

The ! operator can usually be avoided. For example, our hypothetical if-else statement can instead begin with the following, which is equivalent and easier to read:

```
if (x >= y)
    ...
```

We will not have much call to use the ! operator until later in this book, so we will postpone any detailed discussion of it until then.

Sometimes you want one of the two alternatives in an if-else statement to do nothing at all. In C++ this can be accomplished by omitting the else part. These sorts of statements are referred to as if statements to distinguish them from if-else statements. For example, the first of the following two statements is an if statement:

```
if (sales >= minimum)
    salary = salary + bonus;
cout << "salary = $" << salary;
```

If the value of sales is greater than or equal to the value of minimum, the assignment statement is executed and then the following cout statement is executed. On the other hand, if the value of sales is less than minimum, then the embedded assignment statement is not executed, so the if statement causes no change (that is, no bonus is added to the base salary), and the program proceeds directly to the cout statement.

## The "or" Operator ||

You can form a more elaborate Boolean expression by combining two simple tests using the "or" operator ||.

### SYNTAX (FOR A BOOLEAN EXPRESSION USING ||)

```
(Comparison_1) || (Comparison_2)
```

### EXAMPLE (WITHIN AN if-else STATEMENT)

```
if ( (x == 1) || (x == y) )
    cout << "x is 1 or x equals y.\n";
else
    cout << "x is neither 1 nor equal to y.\n";
```

If the value of x is equal to 1 or the value of x is equal to the value of y (or both), then the first cout statement will be executed; otherwise, the second cout statement will be executed.

## PITFALL Strings of Inequalities

Do not use a string of inequalities such as the following in your program:

```
if (x < z < y)
    cout << "z is between x and y.";
```

**Do not do this!**

If you do use this type of expression, your program will probably compile and run, but it will undoubtedly give incorrect output. We will explain why this happens after we learn more details about the C++ language. The same problem will occur with a string of comparisons using any of the comparison operators; the problem is not limited to < comparisons. The correct way to express a string of inequalities is to use the “and” operator && as follows:

```
if ( (x < z) && (z < y) )
    cout << "z is between x and y.";
```

**correct form**

## PITFALL Using = in place of ==

Unfortunately, you can write many things in C++ that you would think are incorrectly formed C++ statements but turn out to have some obscure meaning. This means that if you mistakenly write something that you would expect to produce an error message, you may find out that the program compiles and runs with no error messages, but gives incorrect output. Since you may not realize you wrote something incorrectly, this can cause serious problems. By the time you realize something is wrong, the mistake may be very hard to find. One common mistake is to use the symbol = when you mean ==. For example, consider an if-else statement that begins as follows:

```
if (x = 12)
    Do_Something
else
    Do_Something_Else
```

Suppose you wanted to test to see if the value of x is equal to 12 so that you really meant to use == rather than =. You might think the compiler will catch your mistake. The expression

```
x = 12
```

is not something that is satisfied or not. It is an assignment statement, so surely the compiler will give an error message. Unfortunately, that is not the case. In C++ the expression x = 12 is an expression that returns (or has) a value, just like x + 12 or 2 + 3. An assignment expression’s value is the value transferred to the variable on the left. For example, the value of x = 12 is 12. We saw in our discussion of Boolean value compatibility that int values may be converted to true or false. Since 12 is not zero, it is converted to true. If you use x = 12 as the Boolean expression in an if statement, the Boolean expression is always true, so the first branch (Do_Something) is always executed.

This error is very hard to find because it looks correct! The compiler can find the error without any special instructions if you put the 12 on the left side of the comparison, as in

![](img/88b1f375f11336dbd9dac8b1675d0698_115_0.png)

```
if (12 == x)
    Do_Something;
else
    Do_Something_Else;
```

Then, the compiler will give an error message if you mistakenly use = instead of ==. Remember that dropping one of the = in an == is a common error that is not caught by many compilers, is very hard to see, and is almost certainly not what you wanted. In C++, many executable statements can also be used as almost any kind of expression, including as a Boolean expression for an if-else statement. If you put an assignment statement where a Boolean expression is expected, the assignment statement will be interpreted as a Boolean expression. Of course the result of the “test” will undoubtedly not be what you intended as the Boolean expression. The if-else statement above looks fine at a quick glance and it will compile and run. But, in all likelihood, it will produce puzzling results when it is run.

## Compound Statements

You will often want the branches of an if-else statement to execute more than one statement each. To accomplish this, enclose the statements for each branch between a pair of braces, { and }, as indicated in the second syntax template in Display 2.9 and illustrated in Display 2.11. A list of statements enclosed in a pair of braces is called a compound statement. A compound statement is treated as a single statement by C++ and may be used anywhere that a single statement may be used. (Thus, the second syntax template in Display 2.9 is really just a special case of the first one.) Display 2.11 contains two compound statements, embedded in an if-else statement.

Syntax rules for if-else demand that the Yes statement and No statement be exactly one statement. If more statements are desired for a branch, the statements must be enclosed in braces to convert them to one compound statement. If two or more statements not enclosed by braces are placed between the if and the else, then the compiler will give an error message.

### DISPLAY 2.11 Compound Statements Used With if-else

```
1   if (my_score > your_score)
2   {
3       cout << "I win!\n";
4       wager = wager + 100;
5   }
6   else
7   {
8       cout << "I wish these were golf scores.\n";
9       wager = 0;
10  }
```
