# The puts() Function

In C the puts() function is used to display a string at a time in the standard output device followed by a new character. The general form or the syntax of puts() function is

```
puts(argument) ;
```

The puts() function accepts only a single argument. The argument passed within a function must be a data item. It represents a string or a character array. The string displayed by the puts() function may include white space characters. The puts() function will display only one string at a time.

# 1.9 Decision Making and Branching Statements

In case of C programs, that we have seen so far, the statements are normally executed sequentially as they appear in the program. By default, the statements in the program are executed sequentially. However, in practice we have situations where we may have to change the order of execution of statements until specified conditions are met. These kinds of situations are dealt in C using decision control statements.

One of several possible actions will be carried out depending upon the outcome of the logical test is referred as branching. Some portion of the program has to be executed several number of times or until a particular condition is being met. This is referred as looping. The different decision control or decision-making statements in C are

+   - The if statement
+   - The if-else statement
+   - The switch statement
+   - The conditional operator
+   - The break, continue and goto statements.

# 1.9.1 The if Statement

C uses the keyword if to implement decision control statements. The if statement can be used to check some conditions and execute one or more statements when specified conditions are met. The general form or the syntax of an if statement is

```
if(condition)
{
executable-X-statement(s) ;
}
executable-Y-statement(s) ;
```

Fig. 1.3, shows the operation of an if statement. The condition used in an if statement should be specified within parenthesis. When a program with if statement is evaluated the condition specified after the if statement is executed first. If the condition is true then the executable-X-statement(s) within the flower braces

![](bbox=[0.58, 0.68, 0.92, 0.92])