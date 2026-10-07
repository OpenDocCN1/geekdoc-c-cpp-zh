```
=>// Set the button to indicate an invalid value
}) is not null;
```

The order of precedence is not, and, or; the first two examples don't need parentheses. Parentheses, however, are allowed to change the default order of precedence as demonstrated (arbitrarily) by match expressions in the switch expression of Listing 7.24.

Be aware that using the or and not operators, you cannot also declare a variable. For instance:

```
if (input is "data" or string text) {
```

will result in an error: "CS8780: A variable may not be declared within a ‘not' or ‘or' pattern." Doing so result in ambiguity about whether initialization of text occurred.

# Parenthesized Patterns (C# 9.0)

To override the order of precedence of logical pattern operators you can group them together using parentheses (see Listing 7.26).

Listing 7.26: Parenthesized Patterns

```
public bool IsOutsideOfStandardWorkHours(
    TimeOnly time) =>
    time.Hour is not
    ( 8 and < 17 and not 12); // Parenthesis Pattern - C# 10.
```

Parenthesizing is available with both operators and switch syntax.

# Tuple Patterns (C# 8.0)

With tuple pattern matching, you can check for constant values within the tuple or assign tuple items to a variable (see Listing 7.27).

Listing 7.27: Tuple Pattern Matching with the is Operator

```
public static void Main(params string[] args)
{
```