# ### 3.8.2 Conditional Statements

The conditional statement in Java has the form

```
```java
if (condition) statement
```
```

The condition must be surrounded by parentheses.

In Java, as in most programming languages, you will often want to execute multiple statements when a single condition is true. In this case, use a *block statement* that takes the form

```
```java
{
    statement1
    statement2
    . . .
}
```
```

For example:

```
```java
if (yourSales >= target)
{
    performance = "Satisfactory";
    bonus = 100;
}
```
```

In this code all the statements surrounded by the braces will be executed when yourSales is greater than or equal to target (see Figure 3.7).

> > **NOTE:**
> >
> > A block (sometimes called a *compound statement*) enables you to have more than one (simple) statement in any Java programming structure that otherwise allows for a single (simple) statement.