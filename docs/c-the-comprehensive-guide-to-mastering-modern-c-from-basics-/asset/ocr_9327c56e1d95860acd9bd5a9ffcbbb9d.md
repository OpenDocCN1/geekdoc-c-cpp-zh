# 8.10 The “switch” Statement

You have already seen that you can use if-else cascades to check multiple cases in succession. The switch statement is a specialized form of the case where you always test the same expression, and the expression has an int-like type—or is an enum, as you will see in Chapter 16, Section 16.12.2:

```
switch( Expression ) { Cases }
```

Since C++17, it works analogously to if as well:

```
switch( Initialization ; Expression ) { Cases }
```

Where Cases consist of a sequence of cases of the following form:

```
case Constant: Statements
```

From the list of Cases, those Statements are executed whose Constant matches the result of the Expression. There are still some things to consider or that are worth knowing:

+   * Cases must not contain duplicate Constants, but they do not need to follow a specific order.
* Instead of case, you can also use default once to catch everything else. Normally, this is the last or first case, but it doesn't have to be.
* You can also write multiple case instructions directly in a row without statements in between if you want to combine multiple cases.