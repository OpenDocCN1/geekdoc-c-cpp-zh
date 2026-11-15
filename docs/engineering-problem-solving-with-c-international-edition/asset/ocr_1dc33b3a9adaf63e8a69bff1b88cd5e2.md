Compound statement

If we wish to execute several statements (or a sequence structure) when the condition is true, we use a **compound statement**, or block, which is composed of a set of statements enclosed in braces. The location of the braces is a matter of style; two common styles are shown:

```
Style 1
if (condition)
{
statement 1;
statement 2;
...
statement n;
}

Style 2
if (condition) {
statement 1;
statement 2;
...
statement n;
}
```

![](bbox=[0.145, 0.29, 0.2, 0.33])

In the text solutions, we use the first style convention; thus, both braces are on lines by themselves. Although this makes the program a little longer, it also makes it easier to notice if a brace has been mistakenly omitted. Figure 3.5 contains flowcharts of the control flow with simple `if` statements containing either one statement to execute, or several statements to execute, if the condition is true.

A specific example of an `if` statement follows:

```
if (a < 50)
{
++count;
sum += a;
}
```

![](bbox=[0.25, 0.49, 0.88, 0.87])

Figure 3.5 Flowcharts for selection statements.