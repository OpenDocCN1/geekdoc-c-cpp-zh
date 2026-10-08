your learning right. It is very tempting to dash ahead, focusing on the parts of programming that – like what is described in the rest of this chapter – are concrete and immediately useful and to ignore the "softer" more conceptual parts of the art of software development. However, good programmers and system designers know (often having learned it the hard way) that concerns about structure lie at the heart of good software and that ignoring structure leads to expensive messes. Without structure, you are (metaphorically speaking) building with mud bricks. It can be done, but you'll never get to the fifth floor (mud bricks lack the structural strength for that). If you have the ambition to build something reasonably permanent, you pay attention to matters of code structure and organization along the way, rather than having to come back and learn them after failures.

# # 4.3 Expressions

The most basic building block of programs is an expression. An expression computes a value from a number of operands. The simplest expression is simply a literal value, such as `10`, `'a'`, `3.14`, or `"Norah"`.

Names of variables are also expressions. A variable represents the object of which it is the name. Consider:

```
// compute area:
int length = 20; // a literal integer (used to initialize a variable)
int width = 40;
int area = length*width; // a multiplication
```

Here the literals **20** and **40** are used to initialize the variables **length** and **width**. Then, **length** and **width** are multiplied; that is, we multiply the values found in **length** and **width**. Here, **length** is simply shorthand for "the value found in the object named *length*." Consider also

```
length = 99; // assign 99 to length
```

Here, as the left-hand operand of the assignment, **length** means "the object named **length**", so that the assignment expression is read "Put **99** into the object named by **length**." We distinguish between **length** used on the left-hand side of an assignment or an initialization ("the lvalue of *length*" or "the object named by *length*") and **length** used on the right-hand side of an assignment or initialization ("the rvalue of *length*," the value of the object named by **length**, or just "the value of **length**").

In this context, we find it useful to visualize a variable as a box labeled by its name:

![](bbox=[0.35, 0.87, 0.55, 0.915])