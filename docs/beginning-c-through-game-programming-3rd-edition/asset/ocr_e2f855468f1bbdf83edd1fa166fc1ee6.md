# Using the Logical AND Operator

The logical AND operator, `&&`, lets you join two expressions to form a larger one, which can be evaluated to `true` or `false`. The new expression is true only if the two expressions it joins are true; otherwise, it is false. Just as in English, “and” means both. Both original expressions must be true for the new expression to be true. Here’s a concrete example from the Designers Network program:

```
if (username == "S.Meier" && password == "civilization")
```

The expression `username == "S.Meier" && password == "civilization"` is true only if both `username == "S.Meier"` and `password == "civilization"` are true. This works perfectly because I only want to grant Sid access if he enters both his username and his password. Just one or the other won’t do.

Another way to understand how `&&` works is to look at all of the possible combinations of truth and falsity (see Table 2.3).

**Table 2.3** Possible Login Combinations Using the AND Operator

| username == "S.Meier" | password == "civilization" | username == "S.Meier" && password == "civilization" |
|---|---|---|
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

Of course, the Designers Network program works for other users besides Sid Meier. Through a series of `if` statements with `else` clauses using the `&&` operator, the program checks three different username and password pairs. If a user enters a recognized pair, he is personally greeted.

# Using the Logical OR Operator

The logical OR operator, `||`, lets you join two expressions to form a larger one, which can be evaluated to `true` or `false`. The new expression is true if the first