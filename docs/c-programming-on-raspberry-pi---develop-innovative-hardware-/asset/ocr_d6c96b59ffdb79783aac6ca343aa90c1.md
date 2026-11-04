| Operator | Description |
|---|---|
| x ^ y | bitwise exclusive OR |
| ~x | complement |
| !x | logical NOT |
| x << y | bit shift left |
| x >> y | bit shift right |

# 3.2.5 ● Auto increment/decrement operators

| Operator | Description |
|---|---|
| x++ | increment x by 1 (after) |
| x-- | decrement x by 1 (after) |
| ++x | increment x by 1 (before) |
| --x | decrement x by 1 (before) |
| x += y | increment x by y (same as x = x + y) |
| x -= y | decrement x by y (same as x = x - y) |
| x *= y | multiply x by y (same as x = x * y) |
| x /= y | divide x by y (same as x = x / y) |
| x&= y | bitwise AND x with y (same as x = x & y) |
| x |= y | bitwise OR x with y (same as x = x | y) |
| x ^= y | bitwise Exclusive OR x with y (same as x = x ^ y) |

# 3.2.6 ● Logical operators

| Operator | Description |
|---|---|
| && | Logical AND (used in conditional tests) |
| || | Logical OR (used in conditional tests) |
| ! | Logical NOT |

# 3.2.7 ● Flow control

Flow control statements constitute very important statements in all programming languages. These statements enable programmers to form conditional program executions, selections, and iterations (loops).

# Conditional statements

# if...else

The if...else block of statements are the main conditional statements. The general format of an if...else block is:

```
if(condition is true)
{
    execute these statements
    ----------------
    ....................
}
else
```