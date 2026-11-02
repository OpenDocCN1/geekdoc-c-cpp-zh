are all equivalent in the increment part of the `for` statement. Some C programmers prefer the form `counter++` because the incrementing occurs *after* the loop body executes, and the postincrementing form *seems* more natural. Because the variable being preincremented or postincremented here does not appear in a larger expression, both forms of incrementing have the *same* effect. The two semicolons in the `for` statement are required.

**Common Programming Error 4.3**

Using commas instead of semicolons in a `for` header is a syntax error.

**Error-Prevention Tip 4.3**

Infinite loops are caused when the loop-continuation condition in an iteration statement never becomes false. To prevent infinite loops, ensure that you do not place a semicolon immediately after a `while` statement’s header. In a counter-controlled loop, make sure the control variable is incremented (or decremented) in the loop. In a sentinel-controlled loop, make sure the sentinel value is eventually input.

# 4.5 for Statement: Notes and Observations

+   1. The initialization, loop-continuation condition and increment can contain arithmetic expressions. For example, if `x = 2` and `y = 10`, the statement
+   
+       ```c
+       for (j = x; j <= 4 * x * y; j += y / x)
+       ```
+   
+       is equivalent to the statement
+   
+       ```c
+       for (j = 2; j <= 80; j += 5)
+       ```

+   2. The “increment” may be negative (in which case it’s really a *decrement* and the loop actually counts *downward*).

+   3. If the loop-continuation condition is initially *false*, the loop body does *not* execute. Instead, execution proceeds with the statement following the `for` statement.

+   4. The control variable is frequently printed or used in calculations in the body of a loop, but it need not be. It’s common to use the control variable for controlling iteration while never mentioning it in the body of the loop.

+   5. The `for` statement is flowcharted much like the `while` statement. For example, Fig. 4.4 shows the flowchart of the `for` statement
+   
+       ```c
+       for (unsigned int counter = 1; counter <= 10; ++counter) {
+           printf("%u", counter);
+       }
+       ```
+   
+       This flowchart makes it clear that the initialization occurs only once and that incrementing occurs *after* the body statement each time it’s performed.

**Error-Prevention Tip 4.4**

Although the value of the control variable can be changed in the body of a `for` loop, this can lead to subtle errors. It’s best not to change it.