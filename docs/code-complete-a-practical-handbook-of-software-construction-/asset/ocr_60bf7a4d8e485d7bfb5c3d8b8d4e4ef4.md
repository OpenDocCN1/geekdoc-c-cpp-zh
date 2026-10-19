In this example, you ended with a 0, so the parentheses are balanced. In the next example, the parentheses aren’t balanced:

```
Java Example of Unbalanced Parentheses
if ( ( a < b ) == ( c == d ) ) && !done ) ...
  | |   |   |   | |
0 1 2   1 2   1 0   -1
Read this.
Say this.
```

The 0 before you get to the last closing parenthesis is a tip-off that a parenthesis is missing before that point. You shouldn’t get a 0 until the last parenthesis of the expression.

*Fully parenthesize logical expressions*  Parentheses are cheap, and they aid readability. Fully parenthesizing logical expressions as a matter of habit is good practice.

# Knowing How Boolean Expressions Are Evaluated

Many languages have an implied form of control that comes into play in the evaluation of boolean expressions. Compilers for some languages evaluate each term in a boolean expression before combining the terms and evaluating the whole expression. Compilers for other languages have “short-circuit” or “lazy” evaluation, evaluating only the pieces necessary. This is particularly significant when, depending on the results of the first test, you might not want the second test to be executed. For example, suppose you’re checking the elements of an array and you have the following test:

```
Pseudocode Example of an Erroneous Test
while ( i < MAX_ELEMENTS and item[ i ] <> 0 ) ...
```

If this whole expression is evaluated, you’ll get an error on the last pass through the loop. The variable i equals maxElements, so the expression item[ i ] is equivalent to item[ maxElements ], which is an array-index error. You might argue that it doesn’t matter since you’re only looking at the value, not changing it. But it’s sloppy programming practice and could confuse someone reading the code. In many environments it will also generate either a run-time error or a protection violation.

In pseudocode, you could restructure the test so that the error doesn’t occur:

```
Pseudocode Example of a Correctly Restructured Test
while ( i < MAX_ELEMENTS )
  if ( item[ i ] <> 0 ) then
  ...
```

This is correct because item[ i ] isn’t evaluated unless i is less than maxElements.