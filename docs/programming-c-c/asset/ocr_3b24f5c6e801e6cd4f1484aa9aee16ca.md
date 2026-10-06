# Working with Control Stalements and Loops

The break statement can be used in both switch and loop statements.

The continue statement can appear only in loops. You will get an error if this appears in switch statement.

When a break statement is encountered, it terminates the block and gets the control out of the switch or loop.

When a continue statement is encountered, it gets the control to the next iteration of the loop.

A break causes the innermost enclosing loop or switch to be exited immediately.

A continue inside a loop nested within iteration next loop.

# GOTO STATEMENT IN C

goto is a jump statement used to transfer program control unconditionally from one part of a function to another. I have used the word unconditionally because there is no restriction on control transfer. You can transfer program control from one position to any position within a function. Many programmers use goto to gain full control over their program.

# Syntax of goto statement:

```
label:
goto label;
```

# Parts of goto statement

goto is divided in two parts, label definition and goto keyword.

+   - Label is a valid identifier followed by colon symbol . Each label works as a bookmark to specific location. You are free to define any number of labels anywhere inside a function.

+   - goto is a keyword used with label to transfer program control to the mentioned label. You can only transfer program control to a label within same function. Cross-function control transfer, using goto is not possible and results in compilation error.

There is no restriction in order of goto and label. You are free to define a label anywhere inside a function. For example, both the below examples are valid.

# Label definition above goto statement

```
goto label1;
```