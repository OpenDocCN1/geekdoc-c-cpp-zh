C++ has two Boolean operators that combine conditions: `&&` (and) and `||` (or).

The condition of the test has two parts, joined by the `&&` operator. (As shown in Table 5 and Appendix B, the `>` and `<` operators have higher precedence than the `&&` operator.)

| Operator | Description |
|---|---|
| `++` `--` `+` (unary) `-` (unary) `!` | Increment, decrement, positive, negative, Boolean *not* |
| `*` `/` `%` | Multiplication, division, remainder |
| `+` `-` | Addition, subtraction |
| `<` `<=` `>` `>=` | Comparisons |
| `==` `!=` | Equal, not equal |
| `&&` | Boolean *and* |
| `||` | Boolean *or* |

Each part is a Boolean value that can be true or false. The combined expression is true if both individual expressions are true. If either one of the expressions is false, then the result is also false (see Figure 8).

**A && B**

| A | B | A && B |
|---|---|---|
| true | true | true |
| true | false | false |
| false | true | false |
| false | false | false |

**A || B**

| A | B | A \|\| B |
|---|---|---|
| true | true | true |
| true | false | true |
| false | true | true |
| false | false | false |

**!A**

| A | !A |
|---|---|
| true | false |
| false | true |

# Figure 8  Boolean Truth Tables

Conversely, let’s test whether water is *not* liquid at a given temperature. That is the case when the temperature is at most 0 or at least 100. Use the `||` (or) operator to combine the expressions:

```
```cpp
if (temp <= 0 || temp >= 100) { cout << "Not liquid"; }
```
```

Figure 9 shows flowcharts for these examples.

# EXAMPLE CODE

See sec07 of your companion code for a program that compares numbers using Boolean expressions.

To invert a condition, use the `!` (not) operator.

Sometimes you need to *invert* a condition with the `!` logical operator. The `!` operator takes a single condition and evaluates to true if that condition is false and to false if the condition is true. In this example, output occurs if the value of the Boolean variable frozen is false:

```
```cpp
if (!frozen)
{
    cout << "Not frozen";
}
```
```