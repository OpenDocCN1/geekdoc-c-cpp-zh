
![](img/d61019b035dd82beb581604273c0ee6b_142_0.png)

**Figure 9**  Flowcharts for *and* and *or* Combinations

Table 6 illustrates additional examples of evaluating Boolean operators.

**Table 6 Boolean Operators**

| Expression | Value | Comment |
|---|---|---|
| `0 < 200 && 200 < 100` | `false` | Only the first condition is true. Note that the `<` operator has a higher precedence than the `&&` operator. |
| `0 < 200 \|\| 200 < 100` | `true` | The first condition is true. |
| `0 < 200 \|\| 100 < 200` | `true` | The `\|\|` is not a test for “either-or”. If both conditions are true, the result is true. |
| `0 < 200 < 100` | `true` | **Error:** The expression `0 < 200` is true, which is converted to 1. The expression `1 < 100` is true. You never want to write such an expression; see Common Error 3.5. |
| `-10 && 10 > 0` | `true` | **Error:** −10 is not zero. It is converted to true. You never want to write such an expression; see Common Error 3.5. |
| `0 < x && x < 100 \|\| x == -1` | `(0 < x && x < 100) \|\| x == -1` | The `&&` operator has a higher precedence than the `\|\|` operator. |
| `!(0 < 200)` | `false` | `0 < 200` is true, therefore its negation is false. |
| `frozen == true` | `frozen` | There is no need to compare a Boolean variable with true. |
| `frozen == false` | `!frozen` | It is clearer to use `!` than to compare with false. |

![](img/d61019b035dd82beb581604273c0ee6b_143_0.png)

## Common Error 3.5

### Combining Multiple Relational Operators

Consider the expression

```cpp
if (0 <= temp <= 100) // Error
```

This looks like the mathematical test 0 ≤ temp ≤ 100. Unfortunately, it is not.

Let us dissect the expression `0 <= temp <= 100`. The first half, `0 <= temp`, is a test with outcome true or false, depending on the value of temp. The outcome of that test (true or false) is then compared against 100. Can one compare truth values and floating-point numbers? Is true larger than 100 or not? Unfortunately, to stay compatible with the C language, C++ converts false to 0 and true to 1. Therefore, the expression will always evaluate to true.

You must be careful not to mix logical and arithmetic expressions in your programs.

```cpp
if (0 <= temp && temp <= 100) ...
```

Another common error, along the same lines, is to write

```cpp
if (x && y > 0) ... // Error
```

instead of

```cpp
if (x > 0 && y > 0) ...
```

Unfortunately, the compiler will not issue an error message. Instead, it converts x to true or false. Zero is converted to false, and any nonzero value is converted to true. If x is not zero, then it tests whether y is greater than 0, and finally it computes the and of these two truth values. Naturally, that computation makes no sense.

![](img/d61019b035dd82beb581604273c0ee6b_143_1.png)

## Common Error 3.6

### Confusing && and || Conditions

It is a surprisingly common error to confuse `&&` and `||` conditions. A value lies between 0 and 100 if it is at least 0 and at most 100. It lies outside that range if it is less than 0 or greater than 100. There is no golden rule; you just have to think carefully.

Often the `&&` or `||` is clearly stated, and then it isn't too hard to implement it. But sometimes the wording isn't as explicit. It is quite common that the individual conditions are nicely set apart in a bulleted list, but with little indication of how they should be combined. Consider these instructions for filing a tax return. You can claim single filing status if any one of the following is true:

- You were never married.
- You were legally separated or divorced on the last day of the tax year.
- You were widowed, and did not remarry.

Because the test passes if any one of the conditions is true, you must combine the conditions with or. Elsewhere, the same instructions state that you may use the more advantageous status of married filing jointly if all five of the following conditions are true:

- Your spouse died less than two years ago and you did not remarry.
- You have a child whom you can claim as dependent.
- That child lived in your home for all of the tax year.
- You paid over half the cost of keeping up your home for this child.
- You filed a joint return with your spouse the year he or she died.

Because all of the conditions must be true for the test to pass, you must combine them with an and.

## Special Topic 3.4

### Short-Circuit Evaluation of Boolean Operators

![](img/d61019b035dd82beb581604273c0ee6b_144_0.png)

When the && and || operators are computed, evaluation stops as soon as the truth value is determined. When an && is evaluated and the first condition is false, the second condition is not evaluated, because it does not matter what the outcome of the second test is.

For example, consider the expression

```cpp
quantity > 0 && price / quantity < 10
```

Suppose the value of quantity is zero. Then the test `quantity > 0` fails, and the second test is not attempted. That is just as well, because it is illegal to divide by zero.

Similarly, when the first condition of an || expression is true, then the remainder is not evaluated since the result must be true.

This process is called short-circuit evaluation.

The && and || operators are computed using short-circuit evaluation: As soon as the truth value is determined, no further conditions are evaluated.

![](img/d61019b035dd82beb581604273c0ee6b_144_1.png)

In a short circuit, electricity travels along the path of least resistance. Similarly, short-circuit evaluation takes the fastest path for computing the result of a Boolean expression.

## Special Topic 3.5

### De Morgan's Law

![](img/d61019b035dd82beb581604273c0ee6b_144_2.png)

Humans generally have a hard time comprehending logical conditions with not operators applied to and/or expressions. De Morgan's Law, named after the logician Augustus De Morgan (1806-1871), can be used to simplify these Boolean expressions.

Suppose we want to charge a higher shipping rate if we don't ship within the continental United States.

```cpp
if (!(country == "USA"
    && state != "AK"
    && state != "HI"))
    shipping_charge = 20.00;
```

This test is a little bit complicated, and you have to think carefully through the logic. When it is not true that the country is USA and the state is not Alaska and the state is not Hawaii, then charge $20.00. Huh? It is not true that some people won't be confused by this code.

De Morgan's Law has two forms: one for the negation of an or expression and one for the negation of an and expression

```text
!(A && B) is the same as !A || !B
!(A || B) is the same as !A && !B
```

Pay particular attention to the fact that the `&&` and `||` operators are reversed by moving the not inward. For example, the negation of "the state is Alaska or it is Hawaii",

```cpp
!(state == "AK" || state == "HI")
```

De Morgan's Law tells you how to negate && and || conditions.

When reading a value, check that it is within the required range.

Use the fail function to test whether the input stream has failed.

It is simple to guard against an input of 13:

```cpp
if (floor == 13)
{
    cout << "Error: There is no thirteenth floor." << endl;
    return 1;
}
```

The statement `return 1;` immediately exits the main function and therefore terminates the program. It is a convention to return with the value 0 if the program completed normally, and with a non-zero value when an error was encountered.

Here is how you ensure that the user doesn’t enter a number outside the valid range:

```cpp
if (floor <= 0 || floor > 20)
{
    cout << "Error: The floor must be between 1 and 20." << endl;
    return 1;
}
```

However, dealing with an input that is not a valid integer is a more serious problem.

When the statement `cin >> floor;` is executed, and the user types in an input that is not an integer (such as five), then the integer variable floor is not set. Instead, the input stream cin is set to a failed state. You call the fail member function to test for that failed state.

```cpp
if (cin.fail())
{
    cout << "Error: Not an integer." << endl;
    return 1;
}
```

The order of the if statements is important. You must first test for `cin.fail()`. After all, if the input failed, no value has been assigned to floor, and it makes no sense to compare it against other values.

Input failure is quite serious in C++. Once input has failed, all subsequent attempts at input will fail as well. Special Topic 4.1 shows how to write programs that are more tolerant of bad input. For now, our goal is simply to detect bad input and to exit the program when it occurs.

Here is the complete elevator program with input validation.

**sec08/elevator2.cpp**

```cpp
#include <iostream>

using namespace std;

int main()
{
    int floor;
    cout << "Floor: ";
    cin >> floor;

    // The following statements check various input errors
```
