# FIGURE 6-9 Steps of the for statement

![](bbox=[0.28, 0.12, 0.78, 0.44])

1. The initialize statement is executed first and only once.

> NOTE
> By separating the statements with commas, you can include more than one executable statement in the initialize location. The semicolon ends the initialization portion. Usually, however, the only variable initialized here is the loop control variable.

2. The test is performed. Because the for statement is a pretest loop, the test is performed before the loop body is executed. When the conditional expression evaluates to false, the rest of the for statement (the update and body of the loop) is bypassed and control transfers to the statement following the for statement.

3. When the conditional expression evaluates to true, the body of the loop is performed.

4. The update statement is executed. Often this involves incrementing a variable.

5. Steps 2, 3, and 4 are repeated until the conditional expression evaluates to false.

As stated, Figure 6-9 numbers the steps that a for statement goes through when it executes. The conditional expression is (i < 2). The body of the loop is executed twice for values of i = 0 and i = 1. When i is updated to 2, the conditional expression no longer evaluates to true. The body is bypassed and control transfers to the statement following the for loop.

The for statement is a compact method of writing the same kind of loop that can be written using while; it packages together the initialization, test, and update all on one line. Take, for example, the while statement in Example 6-11 that displays three columns of text for all values between 0 and 10. It displays the counter's value, counter's square, and counter's cubed value.