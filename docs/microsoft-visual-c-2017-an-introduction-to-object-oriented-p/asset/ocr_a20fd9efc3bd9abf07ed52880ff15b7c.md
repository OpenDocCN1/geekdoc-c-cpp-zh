# Making Decisions Using the if-else Statement

Some decisions are dual-alternative decisions; they have two possible resulting actions. If you want to perform one action when a Boolean expression evaluates as true and an alternate action when it evaluates as false, you can use an if-else statement. The if-else statement takes the following form:

```
if(expression)
    statement1;
else
    statement2;
```

You can code an if without an else, but it is illegal to code an else without an if.
Just as you can block multiple statements they all execute when an expression within an if is true, you can block multiple statements after an else so that they will all execute when the evaluated expression is false. For example, the following code assigns 0 to bonus and also produces a line of output when the Boolean variable isUnderBudget is false:

```
if(isProjectUnderBudget)
    bonus = 200;
else
    bonus = 0;
    WriteLine("Notify contractor");
```

Figure 4-10 shows the logic for an if-else statement, and Figure 4-11 shows a program that contains the statement. With every execution of the program, one or the other of the two WriteLine() statements executes. The indentation in the if-else example in Figure 4-11 is not required, but it is standard. You vertically align the keyword if with else, and then indent the action statements that depend on the evaluation. Figure 4-12 shows two executions of the program.