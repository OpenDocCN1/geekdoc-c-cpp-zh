
because > and < have higher precedence than ||. In fact, you could omit all the parentheses in the previous expression and it would have the same meaning, although it would be harder to read. Although we do not advocate omitting all the parentheses, it might be instructive to see how such an expression is interpreted using the precedence rules. Here is the expression without any parentheses:

```
x + 1 > 2 || x + 1 < −3
```

The precedences rules say first apply the unary −, then apply the +’s, then the > and the <, and finally apply the ||, which is exactly what the fully parenthesized version says to do.

The previous description of how a Boolean expression is evaluated is basically correct, but in C++, the computer actually takes an occasional shortcut when evaluating a Boolean expression. Notice that in many cases you need to evaluate only the first of two subexpressions in a Boolean expression. For example, consider the following:

```
(x >= 0) && (y > 1)
```

If x is negative, then (x >= 0) is false. As you can see in the tables in Display 2.1, when one subexpression in an && expression is false, then the whole expression is false, no matter whether the other expression is true or false. Thus, if we know that the first expression is false, there is no need to evaluate the second expression. A similar thing happens with || expressions. If the first of two expressions joined with the || operator is true, then you know the entire expression is true, no matter whether the second expression is true or false. The C++ language uses this fact to sometimes save itself the trouble of evaluating the second subexpression in a logical expression connected with an && or ||. C++ first evaluates the leftmost of the two expressions joined by an && or ||. If that gives it enough information to determine the final value of the expression (independent of the value of the second expression), then C++ does not bother to evaluate the second expression. This method of evaluation is called short-circuit evaluation.

Some languages other than C++ use complete evaluation. In complete evaluation, when two expressions are joined by an && or ||, both subexpressions are always evaluated and then the truth tables are used to obtain the value of the final expression.

Both short-circuit evaluation and complete evaluation give the same answer, so why should you care that C++ uses short-circuit evaluation? Most of the time you need not care. As long as both subexpressions joined by the && or the || have a value, the two methods yield the same result. However, if the second subexpression is undefined, you might be happy to know that C++ uses short-circuit evaluation. Let’s look at an example that illustrates this point. Consider the following:

```
if ( (kids != 0) && ((pieces/kids) >= 2) )
    cout << "Each child may have two pieces!";
```

If the value of kids is not zero, this statement involves no subtleties. However, suppose the value of kids is zero; consider how short-circuit evaluation handles this case. The expression (kids != 0) evaluates to false, so there would be no need to evaluate the second expression. Using short-circuit evaluation, C++ says that the entire expression is false, without bothering to evaluate the second expression. This prevents a run-time error, since evaluating the second expression would involve dividing by zero.

## Pitfall

## INTEGER VALUES CAN BE USED AS BOOLEAN VALUES

C++ sometimes uses integers as if they were Boolean values and bool values as if they were integers. In particular, C++ converts the integer 1 to true and converts the integer 0 to false, and vice versa. The situation is even a bit more complicated than simply using 1 for true and 0 for false. The compiler will treat any nonzero number as if it were the value true and will treat 0 as if it were the value false. As long as you make no mistakes in writing Boolean expressions, this conversion causes no problems. However, when you are debugging, it might help to know that the compiler is happy to combine integers using the Boolean operators &&, ||, and !.

For example, suppose you want a Boolean expression that is true provided that time has not yet run out (in some game or process). You might use the following:

```
!time
```

This sounds right if you read it out loud: “not time greater than limit.” The Boolean expression is wrong, however, and unfortunately, the compiler will not give you an error message. The compiler will apply the precedence rules from Display 2.3 and interpret your Boolean expression as the following:

```
(!time) > limit
```

This looks like nonsense, and intuitively it is nonsense. If the value of time is, for example, 36, what could possibly be the meaning of (!time) > limit? After all, that is equivalent to “not 36.” But in C++, any nonzero integer converts to true and 0 is converted to false. Thus, !36 is interpreted as “not true” and so it evaluates to false, which is in turn converted back to 0 because we are comparing to an int.

What we want as the value of this Boolean expression and what C++ gives us are not the same. If time has a value of 36 and limit has a value of 60, you want the above displayed Boolean expression to evaluate to true (because it is not true that time > limit). Unfortunately, the Boolean expression instead evaluates as follows: (!time) evaluates to false, which is converted to 0, so the entire Boolean expression is equivalent to

```
0 > limit
```

That in turn is equivalent to 0 > 60, because 60 is the value of limit, and that evaluates to false. Thus, the above logical expression evaluates to false, when you want it to evaluate to true.

There are two ways to correct this problem. One way is to use the ! operator correctly. When using the operator !, be sure to include parentheses around the argument. The correct way to write the above Boolean expression is

integers convert to bool

```
!(time > limit)
```

Another way to correct this problem is to completely avoid using the ! operator. For example, the following is also correct and easier to read:

```
if (time <= limit)
```

You can almost always avoid using the ! operator, and some programmers advocate avoiding it as much as possible.

## Self-Test Exercises

- 1. Determine the value, true or false, of each of the following Boolean expressions, assuming that the value of the variable count is 0 and the value of the variable limit is 10. Give your answer as one of the values true or false.
  - a. (count == 0) && (limit < 20)
  - b. count == 0 && limit < 20
  - c. (limit > 20) || (count < 5)
  - d. !(count == 12)
  - e. (count == 1) && (x < y)
  - f. (count < 10) || (x < y)
  - g. !((count < 10) || (x < y)) && (count >= 0)
  - h. ((limit/count) > 7) || (limit < 20)
  - i. (limit > 20) || ((limit > 7)
  - j. ((limit/count) > 7) && (limit < 0)
  - k. (limit < 0) && ((limit/count) > 7)
  - l. (5 && 7) + (16)

- 2. You sometimes see numeric intervals given as
  - 2 < x < 3
  - In C++ this interval does not have the meaning you may expect. Explain and give the correct C++ Boolean expression that specifies that x lies between 2 and 3.

- 3. Consider a quadratic expression, say
  - x² - x - 2

Describing where this quadratic is positive (that is, greater than 0) involves describing a set of numbers that are either less than the smaller root (which is −1) or greater than the larger root (which is 2). Write a C++ Boolean expression that is true when this formula has positive values.

4. Consider the quadratic expression
x² − 4x + 3
Describing where this quadratic is negative involves describing a set of numbers that are simultaneously greater than the smaller root (1) and less than the larger root (3). Write a C++ Boolean expression that is true when the value of this quadratic is negative.

## 2.2 Branching Mechanisms

When you come to a fork in the road, take it.

Attributed to Yogi Berra

## if-else STATEMENTS

An if-else statement chooses between two alternative statements based on the value of a Boolean expression. For example, suppose you want to design a program to compute a week's salary for an hourly employee. Assume the firm pays an overtime rate of one-and-one-half times the regular rate for all hours after the first 40 hours worked. When the employee works 40 or more hours, the pay is then equal to

```
rate*40 + 1.5*rate*(hours - 40)
```

However, if the employee works less than 40 hours, the correct pay formula is simply

```
rate*hours
```

The following if-else statement computes the correct pay for an employee whether the employee works less than 40 hours or works 40 or more hours,

```
if (hours > 40)
    grossPay = rate*40 + 1.5*rate*(hours - 40);
else
    grossPay = rate*hours;
```

The syntax for an if-else statement is given in the accompanying box. If the Boolean expression in parentheses (after the if) evaluates to true, then the statement before the else is executed. If the Boolean expression evaluates to false, the statement after the else is executed.
