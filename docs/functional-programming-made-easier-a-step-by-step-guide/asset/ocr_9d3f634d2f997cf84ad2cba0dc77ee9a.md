The higher the Precedence number, the sooner it’s evaluated. Here * is higher than + and so it’s evaluated first.

In our append definition above, we specified:

```
infixr 5 append as <>
```

That defines the operator <> as the equivalent to calling append infixed with Right Associativity and a Precedence of 5. That means it’s evaluated before any other operators that are part of the same expression that have a lower Precedence, i.e. 4, 3, 2, 1, and 0.

# 3.7.3. Fixity

infix means Infixed Operator, i.e. it comes between it’s two values:

```
l1 <> l2
```

Compare that with the Prefixed equivalent:

```
append l1 l2
```

We can use an Infixed Operator in Prefixed Position and we can use a Function in Infixed Position:

```
(<>) l1 l2 ①
l1 `append` l2 ②
```

① The Operator must be surrounded by Parentheses to be used in Prefixed Position.

② The Function name must be surrounded by Back-ticks to be used in Infixed Position.

Infixing a named Function makes sense when it helps readability, e.g. elem is a Predicate that returns true if a Value is an element of an Array:

```
if 42 `elem` [1, -5, 42] then "YES" else "NO"
```

We can read this as: if 42 is an element of [1, -5, 42]...

# 3.8. Comments

We’ve seen inline comments up to this point, e.g.: