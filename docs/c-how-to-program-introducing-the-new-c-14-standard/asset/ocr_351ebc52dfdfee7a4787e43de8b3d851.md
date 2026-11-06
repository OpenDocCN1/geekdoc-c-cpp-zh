*Using an incorrect relational operator or an incorrect final value of a loop counter in the loop-continuation condition of an iteration statement can cause an off-by-one error.*

![](bbox=[0.119, 0.279, 0.191, 0.335])

# Error-Prevention Tip 5.2

*Using the final value and operator `<=` in a loop’s condition helps avoid off-by-one errors. For a loop that outputs 1 to 10, the loop-continuation condition should be `counter <= 10` rather than `counter < 10` (which causes an off-by-one error) or `counter < 11` (which is correct). Many programmers prefer so-called zero-based counting, in which to count 10 times, `counter` would be initialized to zero and the loop-continuation test would be `counter < 10`.*

![](bbox=[0.119, 0.699, 0.191, 0.754])

# Error-Prevention Tip 5.3

*Write loop conditions carefully to prevent loop counters from overflowing.*