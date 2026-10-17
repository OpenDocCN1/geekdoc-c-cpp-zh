22. In William Shakespeare’s *Hamlet* (Act 3, Scene 1), the main character says “To be, or not to be: that is the question:....” If you write this down as a Boolean expression `2 * $B || !(2 * $B)`, the result of the “Shakespearean” expression is always true for the following code fragment.

```
```text
$B = intval($That_is_the_question) % 2 / 2;
$result = 2 * $B || !(2 * $B);
```
```

where variable `$That_is_the_question` contains numeric values.

23. The Boolean expression `!(!$x > 5)` is equivalent to `$x > 5`.

# 15.9  Review Questions: Multiple Choice

Select the correct answer for each of the following statements.

+   1. Which of the following is **not** a comparison operator?
+      a. `>=`
+      b. `=`
+      c. `<`
+      d. All of the above are comparison operators.

+   2. Which of the following is not a logical operator?
+      a. `&`
+      b. `!`
+      c. All of the above are logical operators.
+      d. None of the above is a logical operator.

+   3. If variable `$x` contains a value of 5, what value does the statement `$y = $x % 2 == 1` assign to variable `$y`?
+      a. `true`
+      b. `false`
+      c. none of the above

+   4. If variable `$x` contains a value of 5, what value does the statement `$y = $x % 2 == 0 || intval($x / 2) == 2` assign to variable `$y`?
+      a. `true`
+      b. `false`
+      c. none of the above

> ¹ William Shakespeare (1564–1616) was an English poet, playwright, and actor. He is often referred to as England's national poet. He wrote about 40 plays and several long narrative poems. His works are counted among the best representations of world literature. His plays have been translated into every major living language and are still performed today.