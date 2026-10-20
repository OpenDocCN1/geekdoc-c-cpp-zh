# 12.6.2 The for Statement

The for statement is the first of the three statements that are available in Bash for repetitive execution of a block of commands in a shell script. These statements are commonly known as loops. The following is a brief description of the statement:

> **Syntax:**
> for variable [in argument-list]
> do
> command-list
> done
> 
> **Purpose:** To execute commands in command-list as many times as the number of items in the argument-list, without the optional part in argument-list, the arguments are supplied at the command line

The items in argument-list are assigned to variable one by one, and the commands in command-list, also known as the body of the loop, are executed for every assignment. This process allows the execution of commands in command-list as many times as the number of items in argument-list. Figure 12.4 illustrates the semantics of the for command. Items may be numbers or words.

The following script in the for_demo1 file shows the use of the for command with optional arguments. The variable people is assigned the words in argument-list one by one, and each time, the value of the variable is echoed until no word remains in the list. At that time, control comes out of the for statement,

![](bbox=[0.15, 0.5, 0.85, 0.75])

FIGURE 12.4 Semantics of the for statement.