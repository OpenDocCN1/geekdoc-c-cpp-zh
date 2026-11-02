# Special Topic 3.4

# Short-Circuit Evaluation of Boolean Operators

![](bbox=[0.12, 0.14, 0.17, 0.25])

When the && and || operators are computed, evaluation stops as soon as the truth value is determined. When an && is evaluated and the first condition is false, the second condition is not evaluated, because it does not matter what the outcome of the second test is.

For example, consider the expression

```
quantity > 0 && price / quantity < 10
```

Suppose the value of quantity is zero. Then the test quantity > 0 fails, and the second test is not attempted. That is just as well, because it is illegal to divide by zero.

Similarly, when the first condition of an || expression is true, then the remainder is not evaluated since the result must be true.

This process is called short-circuit evaluation.

The && and || operators are computed using short-circuit evaluation: As soon as the truth value is determined, no further conditions are evaluated.

![](bbox=[0.77, 0.43, 0.93, 0.62])

In a short circuit, electricity travels along the path of least resistance. Similarly, short-circuit evaluation takes the fastest path for computing the result of a Boolean expression.

# Special Topic 3.5

# De Morgan's Law

![](bbox=[0.12, 0.72, 0.17, 0.84])

Humans generally have a hard time comprehending logical conditions with not operators applied to and/or expressions. De Morgan's Law, named after the logician Augustus De Morgan (1806-1871), can be used to simplify these Boolean expressions.

Suppose we want to charge a higher shipping rate if we don't ship within the continental United States.

```
if (!(country == "USA"
    && state != "AK"
    && state != "HI"))
    shipping_charge = 20.00;
```

This test is a little bit complicated, and you have to think carefully through the logic. When it is not true that the country is USA and the state is not Alaska and the state is not Hawaii, then charge $20.00. Huh? It is not true that some people won't be confused by this code.

De Morgan's Law has two forms: one for the negation of an or expression and one for the negation of an and expression

!(A && B) is the same as !A || !B
!(A || B) is the same as !A && !B

Pay particular attention to the fact that the and and or operators are reversed by moving the not inward. For example, the negation of "the state is Alaska or it is Hawaii",

```
!(state == "AK" || state == "HI")
```

De Morgan's Law tells you how to negate && and || conditions.