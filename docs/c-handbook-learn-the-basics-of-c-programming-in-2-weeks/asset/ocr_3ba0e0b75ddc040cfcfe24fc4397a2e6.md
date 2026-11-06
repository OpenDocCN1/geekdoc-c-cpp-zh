# Chapter 6: The Selection Statements

The Java control statements regulate the Java program’s order of execution. There are three major categories that you need to understand, and they are:

+   1. The selection statements if, if-else and switch statements.
+   2. The loop statements while, do-while and for.
+   3. The transfer statements break, return, try-catch-finally, continue, and assert.

We use any of the mentioned statements (depending on the needs of the program) if you want to alter the default execution order. For the Java basics, we will discuss about the selection statements and a bit of loop statements.

# The Selection Statements

Under this category are: if statement, if-else statement, and switch statement.

# Dealing with the if Statement

The if statement tells the computer to execute a particular block of codes only if the expression within the if statement proves to be true. If the statement is false, then the block of codes will not be executed. The execution will continue for the rest of the codes in the program assuming there are no more selection statements that may prompt the execution due to certain condition.

The if statement follows this syntax:

```
if (<conditional expression>)
<statement action>
```

Look at the sample below:

```
public class SampleIfStatement {

public static void main(String[] args) {
```