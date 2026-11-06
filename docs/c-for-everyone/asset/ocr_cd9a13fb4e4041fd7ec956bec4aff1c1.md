**Practice It** Now you can try these exercises at the end of the chapter: R5.12, P5.16, P5.19.

# Programming Tip 5.3

# Keep Functions Short

![](bbox=[0.079, 0.182, 0.226, 0.245])

There is a certain cost for writing a function. You need to design, code, and test the function. The function needs to be documented. You need to spend some effort to make the function reusable rather than tied to a specific context. To avoid this cost, it is always tempting just to stuff more and more code in one place rather than going through the trouble of breaking up the code into separate functions. It is quite common to see inexperienced programmers produce functions that are several hundred lines long.

As a rule of thumb, a function that is so long that its code will not fit on a single screen in your development environment should probably be broken up.

# Programming Tip 5.4

# Tracing Functions

![](bbox=[0.079, 0.383, 0.226, 0.445])

When you design a complex set of functions, it is a good idea to carry out a manual **walk-through** before entrusting your program to the computer.

Take an index card, or some piece of paper, and write down the function call that you want to study. Write the name of the function and the names and values of the parameter variables, like this:

| `int_name(number * 416)` |
| --- |
|  |
|  |

Then write the names and initial values of the function variables. Write them in a table, since you will update them as you walk through the code.

**`int_name(number * 416)`**

| part | name |
| --- | --- |
| 416 | --- |

We enter the test `part >= 100`. `part / 100` is 4 and `part % 100` is 16. `digit_name(4)` is easily seen to be "four". (Had `digit_name` been complicated, you would have started another sheet of paper to figure out that function call. It is quite common to accumulate several sheets in this way.)

Now `name` has changed to `name + " " + digit_name(part / 100) + " hundred"`, that is "four hundred", and `part` has changed to `part % 100`, or 16.

**`int_name(number * 416)`**

| part | name |
| --- | --- |
| 416 | --- |
| 16 | "four hundred" |