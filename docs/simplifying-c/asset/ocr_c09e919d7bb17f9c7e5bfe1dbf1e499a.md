It can be observed in Figure 1 that regardless of the set of action statements executed, C compiler continues the execution of the next statement after the selection. The two-way selection is implemented in C using the *if* and *else* keywords.

The keyword *if* is used for conditional transfer of control. It is used in combination with an expression that can be evaluated to true or false. There are three variants of *if* statements called simple *if* statement, *if-else* statement, and nested *if* statements. Each of them is used in different situations. The next subsection discusses the usage of simple *if* statement.

# The Simple If Statement

A simple if statement represents a case where an action is to be taken only when a specified condition is true and no action is to be taken in case of false condition. The syntax of simple if statement is as follows:

```
if ( test condition )
Action statements;
```

It can be observed in the preceding syntax that the test condition is always written within parenthesis. It is normally an expression that results to an integer value. Any non-zero value represents true, while a zero value represents false. The test condition is not terminated by a semicolon. In case a semicolon is used, the conditional statement is converted into a *null statement*. From the execution point of view, the null statement does not have any significance. By default, the scope of *if* statement is the statement exactly after the test condition. To increase the scope of *if* statement to multiple statements, we need to enclose the statements within opening and closing curly brackets. The statements when embedded within opening and closing curly brackets are called compound statement. Figure 2 illustrates the logical flow of a simple *if* statement:

![](bbox=[0.35, 0.57, 0.7, 0.74])

▲ Figure 2: Logical Flow of a Simple If Statement

It can be observed in Figure 2 that initially the test condition is evaluated. If the value of the test condition is a positive non-zero (true), then control is transferred to the first statement in the true action statement block. The statements within the true action block are then executed. If the value of test condition is zero, *then* no action is taken. The control is transferred to the next statement in sequence after *if* at completion of the true action block or in case no action is taken. Program 1 illustrates the use of simple *if* statement: