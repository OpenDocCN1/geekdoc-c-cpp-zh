=. + c b a

# Figure 8-1. A right triangle

Suppose we had a triangle with sides a = 4, b = 3, and these values were entered onto pdCalc’s stack. In the CLI, you would see the following:

Top 2 elements of stack (size = 2):
2: 3
1: 4

In order to compute c for this triangle, we would implement the following sequence of instructions: dup * swap dup * + 2 root. After pressing enter, the final result would be Top element of stack (size = 1):
1: 5

If the commands were entered one at a time, we would see the intermediate resultant stack every time we pressed enter. Had we entered all of the commands on a single line and then pressed enter, pdCalc would display each intermediate stack before showing the final