# 2.4 The Fundamental Control Structures of Algorithms — 59

```
while(i<=10)
{
  do {
    sum+=i;
    i++;
  } while(i<=10);
  cout<<'sum='<<sum<<endl;
}
```

# 3. for Statement

The use of for statements is the most flexible. They can be used when the number of loops is either certain or not. The syntax form of a for statement is as follows:

```
for (expression 1; expression 2; expression 3)
statement
```

Figure 2.9 is the flow chart of a for statement.

We can see from Figure 2.9 that the execution flow of a for statement is: first calculate the value of expression 1, and then evaluate expression 2 (loop condition). If expression 2 is true, execute the statements in the loop body once; otherwise quit the loop. After each execution of the loop body, calculate expression 3 and then re-evaluate expression 2 to decide whether to continue the execution or.

+   - Some points about for statements:
- Expression 1, 2, and 3 can be omitted, but you cannot omit the semicolons between them. If you omit the three expressions, the statement becomes:
- for (;;) statement //equals to while (true) statement

```
for (;;) statement //equals to while (true) statement
```

This will become a dead cycle.

![](bbox=[0.103, 0.672, 0.611, 0.866])

Figure 2.9: Execution flow of a for statement.