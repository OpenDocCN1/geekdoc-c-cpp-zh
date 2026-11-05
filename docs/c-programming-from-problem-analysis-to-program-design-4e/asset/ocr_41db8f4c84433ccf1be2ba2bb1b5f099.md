# **TABLE 5-4** Conditional logical AND (&&)

| Expression1 | Expression2 | Expression1 && Expression2 |
|---|---|---|
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

© 2013 Cengage Learning

> > **NOTE**
> >
> > Table 5-4 is sometimes referred to as a truth table.

When combining logical operators with relational tests, developers often make the mistake of omitting the variable for the second and subsequent conditions being tested. In English, you would probably say, “if examScore is greater than 69 and less than 91.” You normally do not repeat the variable being tested. In C#, you must repeat the variable. It is incorrect to write:

```
```csharp
(examScore > 69 < 91)                                     //Invalid
```
```

It is also incorrect to write:

```
```csharp
(69 < examScore < 91)                                      //Invalid
```
```

The correct way to write the expression is:

```
```csharp
((examScore > 69) && (examScore < 91))                     //Correct way
```
```

> > **NOTE**
> >
> > It is not necessary to use the two innermost parentheses. Later in this chapter, in Table 5-7, you will explore the order of operations. The relational operators (< and >) have a higher precedence than the logical && and || operators, meaning the comparisons would be performed prior to the &&. Including the parentheses adds to the readability.

As illustrated in Table 5-5, || only returns a false result when both of the expressions or operands are false. At all other times, when either one of the expressions or operands evaluates to true, the entire compound expression evaluates to true.