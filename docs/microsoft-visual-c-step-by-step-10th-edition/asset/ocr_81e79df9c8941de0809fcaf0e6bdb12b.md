Although this code does the job, it's a little ungainly and verbose. You can simplify this block by using a throw expression together with another operator called the query-colon, or?. The query-colon operator acts like an inline if...else statement for an expression. It is a ternary operator that takes the three operands: a Boolean expression, an expression to evaluate and return if the Boolean expression is true, and another expression to evaluate and return if the Boolean expression is false. You can use it with a throw expression like this:

Click here to view code image

```
string name = nameField.Text !=
    "" ? nameField.Text : throw new Exception("Missing input"); // this
is a throw expression
```

In this case, if the nameField box is not empty, the value of the Text property is stored in the name variable. Otherwise, the throw expression is evaluated, which in turns an exception. This code is much more concise than the previous example.

# Using a finally block

When an exception is thrown, it changes the flow of execution through the program. So, you can't guarantee that a statement will always run when the previous statement finishes because the previous statement might throw an exception. In this case, after the catch handler has run, the flow of control resumes at the next statement in the block holding this handler and not at the statement immediately following the code that raised the exception.

Look at the example that follows, which is adapted from the code in Chapter 5, "Using compound assignment and iteration statements.\ It’s very easy to assume that the call to reader.Dispose will always occur when the while loop completes. All, it’s right in the code.

Click here to view code image

```
TextReader reader = ...;
...
string line = reader.ReadLine();
while (line is not null)
{
    line = reader.ReadLine();
```