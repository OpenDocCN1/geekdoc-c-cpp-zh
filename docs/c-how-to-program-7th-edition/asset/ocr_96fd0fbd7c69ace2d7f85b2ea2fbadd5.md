# ### Terminology

+   - !, logical NOT operator 189
+   - &&, logical AND operator 187
+   - ||, logical OR operator 188
+   - ASCII (American Standard Code for Information Interchange) character set 180
+   - bool alpha stream manipulator 190
+   - break statement 185
+   - case label 181
+   - char fundamental type 179
+   - comma operator 168
+   - constant integral expression 176
+   - continue statement 186
+   - controlling expression of a switch 181
+   - decrement a control variable 164
+   - default case in switch 181
+   - definition 165
+   - field width 173
+   - final value of a control variable 164
+   - for repetition statement 166
+   - increment a control variable 164
+   - initial value of a control variable 164
+   - left justified 174
+   - left stream manipulator 174

+   - logical AND (&&) 187
+   - logical negation (!) 189
+   - logical NOT (!) 189
+   - logical operator 187
+   - logical OR (||) 188
+   - loop-continuation condition 164
+   - lvalue ("left value") 192
+   - name of a control variable 164
+   - nesting loop 194
+   - off-by-one error 167
+   - pow standard library function 173
+   - right justified 175
+   - right stream manipulator 174
+   - rvalue ("right value") 192
+   - scope of a variable 168
+   - setw stream manipulator 173
+   - short-circuit evaluation 189
+   - simple condition 187
+   - stacking loop 194
+   - sticky setting 174
+   - switch multiple-selection statement 176
+   - truth table 188
+   - zero-based counting 167

# ### Self-Review Exercises

+   - **5.1** State whether the following are *true* or *false*. If the answer is *false*, explain why.
+     - a. The default case is required in the switch selection statement.
+     - b. The break statement is required in the default case of a switch selection statement to exit the switch properly.
+     - c. The expression ( x > y && a < b ) is true if either the expression x > y is true or the expression a < b is true.
+     - d. An expression containing the || operator is true if either or both of its operands are true.

+   - **5.2** Write a C++ statement or a set of C++ statements to accomplish each of the following:
+     - a. Sum the odd integers between 1 and 99 using a for statement. Assume the integer variables sum and count have been declared.
+     - b. Print the value 333.546372 in a 15-character field with precisions of 1, 2 and 3. Print each number on the same line. Left-justify each number in its field. What three values print?
+     - c. Calculate the value of 2.5 raised to the power 3 using function pow. Print the result with a precision of 2 in a field width of 10 positions. What prints?
+     - d. Print the integers from 1 to 20 using a while loop and the counter variable x. Assume that the variable x has been declared, but not initialized. Print only 5 integers per line. [*Hint*: When x % 5 is 0, print a newline character; otherwise, print a tab character.]
+     - e. Repeat Exercise 5.2(d) using a for statement.

+   - **5.3** Find the errors in each of the following code segments and explain how to correct them.
+     - a.

```
```
x = 1;
while ( x <= 10 ) ;
   x++;
}
```
```