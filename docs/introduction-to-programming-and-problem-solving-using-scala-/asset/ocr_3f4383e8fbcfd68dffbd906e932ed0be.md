# Introduction to Programming and Problem-Solving Using Scala

critical for problem solving in general. Conditional execution gives you the ability to express logic and solve much more complex problems than you could without.

# 3.2 The if Expression

Virtually all programming languages have a construct in them called if. For this construct, you have a condition where one thing should happen if the condition is true. If the condition is false, then neither nor something different will happen. In non-functional languages, the if is a statement. It has no value and simply determines what code will be executed. In Scala and other functional languages, the if is an expression which gives back a value. Scala allows you to use it in either way. The syntax of an if is: (condition) true falseExpression. The else is optional.

Let us start with an example, then we can broaden it to the more general syntax. Take the ticket price example and consider just the person's age. Say we want to consider whether a person should pay the $20's rate or the $35 rate. For our purposes, a child is under the age of 13. We could make a variable with the correct value by this declaration using an if expression.

```
cost = if (age<13) 20 else 35
```

This assumes that age is an Int variable that has been defined prior to this point. The first part of this line is a basic declaration as discussed in chapter 2. The next part contains an expression which checks the age and gives back one of two values depending on whether age<13 is true or false.

When using an expression we always need to include an else because there has to be a value that is given to the variable if the condition is false. This type of behavior can also be accomplished with a var using the if as a statement.

```
var cost=20
if (age>=13) cost=35
```

This code creates a var and gives it the value of 20. It then checks if the age is greater than equal to 13 and if, it changes the value to 35. Note that with this usage, the else clause is not required. Here we only need to do something if the condition is true. In Scala you should prefer the first approach. It is shorter, cleaner, and leaves you with a val which you can not be changed after it is created. The first approach is a functional approach while the second is an imperative approach.

In, format of the if is as follows:

The square brackets denote that the else and the second expression are optional. The condition must be surrounded by parentheses and can be replaced by any expression of type Boolean. The expressions expr1 and expr2 can be any expression you want, though they should typically have the same type.

Often, or both of the expressions will need to be more complex. Consider the time conversion from section 2.9. There are a few places where we could have used conditionals in that example, but a major one would have to check if the user input was a positive value, as what we does not make much sense for negative values. There are