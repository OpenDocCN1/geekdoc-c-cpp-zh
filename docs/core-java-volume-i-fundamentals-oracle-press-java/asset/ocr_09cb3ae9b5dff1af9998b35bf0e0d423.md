These two forms of `switch` are *statements*. In [Section 3.5.9, “Switch Expressions,”] on p. 58, you saw a `switch` *expression*, which yields a value. It doesn’t have the fallthrough behavior.

For symmetry, Java 14 also introduces a `switch` expression with fallthrough, for a total of four forms of `switch`. [Table 3.7] shows them all.

In the fallthrough variants, each case ends with a colon. If the cases end with arrows `->`, then there is no fallthrough. You can’t mix colons and arrows in a single `switch` statement.

Note the `yield` keyword with `switch` expressions. Like `break`, it terminates execution. Unlike `break`, it also yields a value—the value of the expression.

To use statements in a branch of a `switch` expression without fallthrough, you must use braces and `yield`, as in the example in the table that adds a logging statement to a branch:

```
```java
case "Spring" ->
    {
        System.out.println("spring time!");
        yield 6;
    }
```
```

Each branch of a `switch` *expression* must yield a value. Most commonly, each value follows an `->` arrow:

```
```java
case "Summer", "Winter" -> 6;
```
```

If that is not possible, use a `yield` statement.

# **Table 3.7** The four forms of `switch`