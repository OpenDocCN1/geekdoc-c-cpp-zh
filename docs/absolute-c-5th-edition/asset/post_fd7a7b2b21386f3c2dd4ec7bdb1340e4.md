
## PITFALL: Integer Values Can Be Used as Boolean Values

C++ sometimes uses integers as they were Boolean values and bool values as if they were integers. In particular, C++ converts the integer 1 to true and converts the integer 0 to false, vice versa. The situation is a bit more complicated than simply using 1 for true and 0 for false. The compiler will convert any nonzero number as if it were the value true and convert 0 as it were the value false. As long as you make no mistakes in writing Boolean expressions, this conversion causes no problems. However, when you are debugging, it might help to know that the compiler is combining integers using the Boolean operators &&, || and !.

For example, suppose you want a Boolean expression that is provided that time has not yet out (in some game or process). You might use the following:

```
!time > limit
```

This sounds like you read it out: "not greater than limit." The Boolean expression is wrong, however, and unfortunately, the compiler will not give you an error message. The compiler will apply the precedence rules from Display 2.3 and interpret your Boolean expression as the following:

```
(time) > limit
```

This looks like nonsense, and intuitively it is nonsense. If the value of time is, for example, 36, what could possibly be the meaning of (time)? After all, it is equivalent to "not 36". In C++, any nonzero integer converts to true and 0 is converted to false. Thus, !36 is interpreted as "not true" and so it evaluates to false, which is in turn converted back to 0 because we are comparing to int.

What we mean by this Boolean expression and what C++ gives us are not the same. If time has a value of 36 and limit has a value of 0, the previously displayed Boolean expression evaluates to true (because it is not true time > limit). Unfortunately, the Boolean expression instead evaluates as: (time) evaluates to false, which is equivalent to 0, so the entire Boolean expression is equivalent to

```
0 > limit
```

That is equivalent to 0 > 60, because 60 is the value of limit, and evaluates to false. Thus, the above logical expression evaluates to false, when you want it to evaluate to true.

There are two ways to correct this problem. One way is to use the operator correctly. When using the ! operator, be sure to include parentheses around the argument. The correct way to write the above Boolean expression is

```
!(time > limit)
```

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_83_0.png)

## PITFALL: (continued)

Another way to correct this problem is to completely avoid using the ! operator. The example, the following is also correct and easier to read:

```
time <= limit;
```

You can almost always avoid using the ! operator, and some programmers advocate avoiding it as much as possible.

Both short-circuit evaluation and complete evaluation give the same answer, so why you should care that C++ uses short-circuit evaluation? Most of the time you need not care. As long as subexpressions joined by the && or || have a value, the methods yield the same result. If the subexpression is undefined, you might be happy to know that C++ uses short-circuit evaluation. Let's look at an example that illustrates this point:

```
(kids != 0) && ((pieces/kids) >= 2 )
out << "Each child may have two pieces!"
```

If the value of kids is not zero, this statement has no subtleties. However, suppose the value of kids is zero: consider how short-circuit evaluation handles this case. The expression (kids!=0) evaluates to false, there would be no need to evaluate the second expression. Using short-circuit evaluation, C++ says that the entire expression is false, without bothering to evaluate the second expression. This prevents a runtime error, ensuring that the second expression would not divide by zero.

## Self-Test Exercises

1. Determine the value, true or false, each of the following Boolean expressions, assuming that the value of the variable count is 0 and give your answer as one of the values of true or false.
   a. (count == 0) && (limit < 20)
   b. count == 0 && limit < 20
   c. (limit > 20) || (count < 5)
   d. (count == 12)
   e. (count == 1) && (x < y)
   f. (count < 10) || (x < y)
   g. ((count < 10) || ((limit / count) > 7) || (limit < 20))
   h. ((limit / count) > 7) || (limit < 20)
   i. (limit / ((limit / count) > 12)
   j. ((limit / count) > 7) && (limit < 0)
   k. (limit < 0) && ((limit / count) > 7)
   l. (5 & 7) + (!6)

2. You sometimes use numeric intervals given as

2 < x < 3

In C++ this interval does not have the meaning you may expect. Explain and give the C++ Boolean expression that specifies that x lies between 2 and 3.

3. Consider a quadratic expression, say

x² - x - 2

Describing where this quadratic is positive (that is, greater than 0) involves describing a set of numbers that are less than the smaller root (which is -1) or greater than the larger root (which is 2). Write a C++ Boolean expression that is true when this formula has positive values.

4. Consider the quadratic expression

x² - 4x + 3

Describing where this quadratic is negative involves describing a set of numbers that are simultaneously greater than the smaller root (1) and less than the larger root (3). Write a C++ Boolean expression that is true when the value of this quadratic is negative.

## 2.2 Branching Mechanisms

When you come to a fork in the road, take it.

> Attributed to YOGI BERRA

## if-else Statements

An if-else statement chooses between two alternative statements based on the value of a Boolean expression. For example, suppose you want to design a program to compute a week's salary for an hourly employee. Assume the firm pays an overtime rate of one-and-one-half times the regular rate for all hours after the first 40 hours worked. When the employee works 40 or more hours, the pay is equal to

```
rate * 40 + 1.5 * (hours - 40)
```

## if-else Statement

An if-else statement chooses between two alternative statements based on the value of a Boolean expression. For example, suppose you want to design a program to compute a week's salary for an hourly employee. Assume the firm pays an overtime rate of one-and-one-half times the regular rate for all hours after the first 40 hours worked. When the employee works 40 or more hours, the pay is equal to

```
rate * 40 + 1.5 * (hours - 40)
```

## Flow of Control

However, if the employee works less than 40 hours, the correct pay formula is simply

rate * hours

The following if-else statement computes the correct pay for an employee whether the employee works less than 40 hours or works 40 hours or more,

```
if (hours > 40)
Pay = rate * 40 + 1.5 * (hours - 40);
else
grossPay = rate * hours;
```

## Compound Statements

You will want the branches of an if-else statement to execute more than one statement. To accomplish this, enclose the statements for each branch between a pair of braces, { and }, as indicated in the second syntax template in the box entitled "if-else Statement." A list of statements enclosed in a pair of braces is called a compound statement. A compound statement is treated as a single statement by C++ and may be used anywhere that a single statement may be used. (Thus, the second syntax template in the box entitled "if-else Statement" is really just a special case of the first.)

There are two commonly used ways of indenting and placing braces in if-else statements, which are illustrated:

```
if (myScore > yourScore)
{
    cout << "I win!\n";
    wager = wager + 100;
}
else
{
    cout << "I wish these were golf scores.\n";
    wager = 0;
}

The syntax for an if-else statement is given in the accompanying box. If the Boolean expression in parentheses (after the if) evaluates to true, then the statement before the else is executed. If the Boolean expression evaluates to false, the statement after the else is executed.

## EXAMPLE

```
if (myScore > yourScore)
{
    cout << "I win!\n";
    wager = wager + 100;
}
else
{
    cout << "I wish these were golf scores.\n";
    wager = 0;
}
```
