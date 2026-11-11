
The Math class provides several methods to make integer arithmetic safer. The mathematical operators quietly return wrong results when a computation overflows. For example, one billion times three (1000000000 * 3) evaluates to -1294967296 because the largest int value is just over two billion. If you call `Math.multiplyExact(1000000000, 3)` instead, an exception is generated. You can catch that exception or let the program terminate rather than quietly continue with a wrong result. There are also methods `addExact`, `subtractExact`, `incrementExact`, `decrementExact`, `negateExact`, and `absExact`, all with int and long parameters.

### 3.5.3 Conversions between Numeric Types

It is often necessary to convert from one numeric type to another. [Figure 3.1](#figure-3-1) shows the legal conversions.

![](img/0e7b74ef51a065c077b42cd87b362288_92_0.png)

**Figure 3.1** Legal conversions between numeric types

The six solid arrows in [Figure 3.1](#figure-3-1) denote conversions without information loss. The three dotted arrows denote conversions that may lose precision.

For example, a large integer such as `123456789` has more digits than the `float` type can represent. When the integer is converted to a `float`, the resulting value has the correct magnitude but loses some precision.

```java
int n = 123456789;
float f = n; // f is 1.23456792E8
```

When two values are combined with a binary operator (such as `n + f` where `n` is an integer and `f` is a floating-point value), both operands are converted to a common type before the operation is carried out.

- If either of the operands is of type `double`, the other one will be converted to a `double`.
- Otherwise, if either of the operands is of type `float`, the other one will be converted to a `float`.
- Otherwise, if either of the operands is of type `long`, the other one will be converted to a `long`.
- Otherwise, both operands will be converted to an `int`.

### 3.5.4 Casts

In the preceding section, you saw that `int` values are automatically converted to `double` values when necessary. On the other hand, there are obviously times when you want to consider a `double` as an integer. Numeric conversions are possible in Java, but of course information may be lost. Conversions in which loss of information is possible are done by means of *casts*. The syntax for casting is to give the target type in parentheses, followed by the variable name. For example:

```java
double x = 9.997;
int nx = (int) x;
```

Now, the variable `nx` has the value 9 because casting a floating-point value to an integer discards the fractional part.

If you want to *round* a floating-point number to the *nearest* integer (which in most cases is a more useful operation), use the `Math.round` method:

```java
double x = 9.997;
int nx = (int) Math.round(x);
```

Now the variable `nx` has the value 10. You still need to use the cast `(int)` when you call `round`. The reason is that the return value of the `round` method is a `long`, and a `long` can only be assigned to an `int` with an explicit cast because there is the possibility of information loss.

> **CAUTION:**
>
> If you try to cast a number of one type to another that is out of range for the target type, the result will be a truncated number that has a different value. For example, `(byte) 300` is actually 44.

> **C++ NOTE:**
>
> You cannot cast between `boolean` values and any numeric type. This convention prevents common errors. In the rare case when you want to convert a `boolean` value to a number, you can use a conditional expression such as `b ? 1 : 0`.

### 3.5.5 Assignment

There is a convenient shortcut for using binary operators in an assignment. For example,

```text
3 == 7
```

is `false`.

Use `!=` for inequality. For example, the value of

```text
3 != 7
```

is `true`.

Finally, you have the usual < (less than), > (greater than), <= (less than or equal), and >= (greater than or equal) operators. Java, following C++, uses && for the logical “and” operator and || for the logical “or” operator. As you can easily remember from the != operator, the exclamation point ! is the logical negation operator. The && and || operators are evaluated in “short circuit” fashion: The second argument is not evaluated if the first argument already determines the value. If you combine two expressions with the && operator,

```text
expression₁  &&  expression₂
```

and the truth value of the first expression has been determined to be `false`, then it is impossible for the result to be `true`. Thus, the value for the second expression is *not* calculated. This behavior can be exploited to avoid errors. For example, in the expression

```text
x != 0 && 1 / x > x + y // no division by 0
```

the second part is never evaluated if x equals zero. Thus, 1 / x is not computed if x is zero, and no divide-by-zero error can occur.

Similarly, the value of *expression₁ || expression₂* is automatically true if the first expression is true, without evaluating the second expression.

### 3.5.8 The Conditional Operator

Java provides the *conditional* ?: operator that selects a value, depending on a Boolean expression. The expression *condition* ? *expression1* : *expression2* evaluates to the first expression if the condition is true, to the second expression otherwise. For example,

```text
x < y ? x : y
```

gives the smaller of x and y.

### 3.5.9 Switch Expressions

If you need to choose among more than two values, then you can use a switch expression (as of Java 14). It looks like this:

```java
String seasonName = switch (seasonCode)
{
    case 0 -> "Spring";
    case 1 -> "Summer";
    case 2 -> "Fall";
    case 3 -> "Winter";
    default -> "???";
};
```

The case labels can also be strings or constants of an enumerated type.

> **NOTE:**
> The switch expression, like every expression, has a value. Note the -> arrow preceding the value in each branch.

> **NOTE:**
> As of Java 14, there are four (!) forms of `switch`. This section focuses on the most useful one. See Section 3.8.5, “Multiple Selections with `switch`,” on p. 98 for a thorough discussion of all forms of `switch` expressions and statements.

You can provide multiple labels for each `case`, separated by commas:

```java
int numLetters = switch (seasonName)
    {
        case "Spring", "Summer", "Winter" -> 6;
        case "Fall" -> 4;
        default -> -1;
    };
```

When you use the `switch` expression with enumerated constants, you need not supply the name of the enumeration in each label—it is deduced from the switch value. For example:

```java
enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE }; . . .
Size itemSize = . . .;
String label = switch (itemSize)
    {
        case SMALL -> "S"; // no need to use Size.SMALL
        case MEDIUM -> "M";
        case LARGE -> "L";
        case EXTRA_LARGE -> "XL";
    };
```

In the example, it was legal to omit the `default` since there was a case for each possible value.

> **CAUTION:**
> A switch expression with an integer or `String` operand must always have a default since it must yield a value, no matter what the operand value is.

> **CAUTION:**
> If the operand is `null`, a `NullPointerException` is thrown.

### 3.5.10 Bitwise Operators

For any of the integer types, you have operators that can work directly with the bits that make up the integers. This means that you can use masking techniques to get at individual bits in a number. The bitwise operators are

- `&`（“and”）
- `|`（“or”）
- `^`（“xor”）
- `~`（“not”）

These operators work on bit patterns. For example, if n is an integer variable, then

```java
int fourthBitFromRight = (n & 0b1000) / 0b1000;
```

gives you a 1 if the fourth bit from the right in the binary representation of n is 1, and 0 otherwise. Using & with the appropriate power of 2 lets you mask out all but a single bit.

> **NOTE:**
> When applied to boolean values, the `&` and `|` operators yield a boolean value. These operators are similar to the `&&` and `||` operators, except that the `&` and `|` operators are not evaluated in “short circuit” fashion—that is, both arguments are evaluated before the result is computed.
