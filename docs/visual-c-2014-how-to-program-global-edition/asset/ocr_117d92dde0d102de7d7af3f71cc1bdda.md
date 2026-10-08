# 234 Chapter 6 Control Statements: Part 2

+   1. a control variable (or loop counter),
2. the control variable's initial value,
3. the control variable's increment that's applied during each iteration of the loop,
4. loop-continuation condition that determines looping should continue.

Consider the application of Fig. 6.1, which uses a loop to display the numbers from 1 through 10.

| 1 2 3 4 5 6 7 8 9 10 |

Fig. 6.1 | Counter-controlled iteration with the while iteration statement.

In Fig. 6.1, the elements of counter-controlled iteration are defined in lines 9, 11 and 14. Line 9 declares the control variable (counter) as an int, reserves space for it in memory and sets its initial value to 1.
Line 13 displays control variable counter's value iteration of the loop, for each iteration of the loop. The while's loopcondition (line 11) tests whether the value of the control variable is less than or equal to 10 (the final value for which the condition is true). The program performs the while's body even when the control variable exceeds 10 (that is, when counter becomes 11).

> Error-Prevention Tip 6.I
Floating-point values are approximate, so counting loops with floating-point variables of types float or double can result in imprecise counter values and inaccurate counter tests for termination. Use integer values to control counter loops.