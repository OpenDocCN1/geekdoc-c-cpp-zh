# 1.9 CONTROL STATEMENTS

Till now we know that the code in the C program is executed sequentially from the first line of the program to its last line. That is, the second statement is executed after the first, the third statement is executed after the second, so on and so forth. Although this is true, in some cases we want only selected statements to be executed. Control flow statements enable programmers to conditionally execute a particular block of code. There are three types of control statements: decision control (branching), iterative (looping), and jump statements. While branching means deciding what actions have to be taken, looping, on the other hand, decides how many times the action has to be taken. Jump statements transfer control from one point to another point.

# 1.9.1 Decision Control Statements

C supports decision control statements that can alter the flow of a sequence of instructions. These statements help us to jump from one part of the program to another depending on whether a particular condition is satisfied or not. These decision control statements include:

+   - (a) if statement,
+   - (b) if-else statement,
+   - (c) if-else-if statement, and
+   - (d) switch-case statement.

# If Statement

if statement is the simplest decision control statement that is frequently used in decision making. The general form of a simple if statement is shown in Fig. 1.2.

![](bbox=[0.24, 0.48, 0.81, 0.73])

Figure 1.2 if statement construct

The if block may include 1 statement or n statements enclosed within curly brackets. First the test expression is evaluated. If the test expression is true, the statements of the if block are executed, otherwise these statements will be skipped and the execution will jump to statement x.

The statement in an if block is any valid C language statement, and the test expression is any valid C language expression that evaluates to either true or false. In addition to simple relational expressions, we can also use compound expressions formed using logical operators. Note that there is no semi-colon after the test expression. This is because the condition and statement should be put together as a single statement.