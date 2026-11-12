and for compound actions as

```
```
if (expression)
{
    statements
}
else
{
    statements
}
```
```

+   - One special use of the if statement warrants another style. Nested if statements that choose among three or more different courses of action, such as

```
```
if (condition1)
    action1;
else if (condition2)
    action2;
else if (condition3)
    action3;
```
```

are written as

```
```
if (condition1)
    action1;
else if (condition2)
    action2;
else if (Condition3)
    action3;
```
```

This indentation style better reflects the nature of the construct, which is like a generalized switch statement:

```
```
case condition1: action1; break;
case condition2: action2; break;
case condition3: action3; break;
```
```

+   - Braces are used to increase readability, even when they are not a syntactic necessity. For example, in the construct

```
```
while (expression)
{
    if (condition)
        statement1
    else
        statement2
} // end while
```
```

the braces are syntactically unnecessary, because an if is a single statement. However, the braces highlight the scope of the while loop.

# ## B.2.7 Documentation

A program should be well documented so that others can read, use, and modify it easily. Many acceptable styles for documentation are in use today, and exactly what you should include often depends on the particular program or your individual circumstances.

This book will use a special form of documentation comment, called a javadoc-style comment because it originated with the JavaTM programming language. These comments start with /** and end with */ and contain tags that classify different parts of your documentation. Several utility programs are available to read these comments and generate HTML-based documentation. One of these

Highly formatted, HTML-based documentation is easy to produce