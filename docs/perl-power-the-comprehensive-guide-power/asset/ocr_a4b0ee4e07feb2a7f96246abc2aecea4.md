statement transforms the compound statement into what is known as a _conditional_ block. Conditional blocks usually create compound statements; at the same time, you often introduce compound statements using control statements.

# # Control Statements

Control statements provide the entryways to conditional statements or blocks of statements. As Figure 10.1 illustrates, a control statement consists of a word that designates the type of control you want to apply to a given block of statements. Figure 10.1 illustrates an `if` control statement. Logical expressions characterize control statements. The logical expression usually appears between parentheses that follow a keyword that identifies the control statement. A logical operator characterizes the logical expression that appears between the parentheses.

Following the control designation and its accompanying logical expression, you usually encounter the opening brace of the two braces that establish the scope of a controlled block of statements. Whether the block of statements enters the flow of your program depends on the behavior of the control statement.

![](bbox=[0.1445, 0.4438, 0.9277, 0.6562])

# # Program Flow

Program flow consists of the path of logic your program follows when you execute it. The path of logic can vary from program execution to program execution due to the logical decisions you embed in your program. Control statements embody logical decisions, but both using and not using control statements serve to guide the flow of your program. Given this situation, three patterns of activity characterize the flow of most programs:

+   * Sequence. The statements a program contains execute one after another. It might be said that statements execute as the program presents them, but if you use `goto` operators to call