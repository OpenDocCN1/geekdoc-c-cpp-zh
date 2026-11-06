
## Common Error 3.5

### Combining Multiple Relational Operators

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_134_0.png)

Consider the expression

```
if (0 <= temp <= 100) // Error
```

This looks just like the mathematical test 0 ≤ temp ≤ 100. Unfortunately, it is not.

Let us dissect the expression 0 <= temp <= 100. The first half, 0 <= temp, is a test with outcome true or false, depending on the value of temp. The outcome of that test (true or false) is then compared against 100. Can one compare truth values and floating-point numbers? Is true larger than 100 or not? Unfortunately, to stay compatible with the C language, C++ converts false to 0 and true to 1. Therefore, the expression will always evaluate to true.

You must be careful not to mix logical and arithmetic expressions in your programs. Instead, use *and* to combine two separate tests:

```
if (0 <= temp && temp <= 100) ...
```

Another common error, along the same lines, is to write

```
if (x && y > 0) ... // Error
```

instead of

```
if (x > 0 && y > 0) ...
```

Unfortunately, the compiler will not issue an error message. Instead, it converts x to true or false. Zero is converted to false, and any nonzero value is converted to true. If x is not zero, then it tests whether y is greater than 0, and finally it computes the *and* of these two truth values. Naturally, that computation makes no sense.

## Common Error 3.6

### Confusing && and || Conditions

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_134_1.png)

It is a surprisingly common error to confuse *and* and *or* conditions. A value lies between 0 and 100 if it is at least 0 and at most 100. It lies outside that range if it is less than 0 or greater than 100. There is no golden rule; you just have to think carefully.

Often the *and* or *or* is clearly stated, and then it isn't too hard to implement it. But sometimes the wording isn't as explicit. It is quite common that the individual conditions are nicely set apart in a bulleted list, but with little indication of how they should be combined. Consider these instructions for filing a tax return. You can claim single filing status if *any* one of the following is true:

- You were never married.
- You were legally separated *or* divorced on the last day of the tax year.
- You were widowed, *and* did not remarry.

Since the test passes if *any* one of the conditions is true, you must combine the conditions with *or*. Elsewhere, the same instructions state that you may use the more advantageous status of married filing jointly if *all* five of the following conditions are true:

- Your spouse died less than two years ago *and* you did not remarry.
- You have a child whom you can claim as dependent.
- That child lived in your home for *all* of the tax year.
- You paid over *half* the cost of keeping up your home for this child.
- You filed a joint return with your spouse the year he *or* she died.

Because *all* of the conditions must be true for the test to pass, you must combine them with an *and*.

## Special Topic 3.4

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_135_0.png)

### Short-Circuit Evaluation of Boolean Operators

When the && and || operators are computed, evaluation stops as soon as the truth value is determined. When an && is evaluated and the first condition is false, the second condition is not evaluated, because it does not matter what the outcome of the second test is.

> The && and || operators are computed using short-circuit evaluation: As soon as the truth value is determined, no further conditions are evaluated.

For example, consider the expression

```
quantity > 0 && price / quantity < 10
```

Suppose the value of quantity is zero. Then the test quantity > 0 fails, and the second test is not attempted. That is just as well, because it is illegal to divide by zero.

Similarly, when the first condition of an || expression is true, then the remainder is not evaluated since the result must be true.

This process is called short-circuit evaluation.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_135_1.png)

> In a short circuit, electricity travels along the path of least resistance. Similarly, short-circuit evaluation takes the fastest path for computing the result of a Boolean expression.

## Special Topic 3.5

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_135_2.png)

### De Morgan's Law

Humans generally have a hard time comprehending logical conditions with not operators applied to and/or expressions. De Morgan's Law, named after the logician Augustus De Morgan (1806-1871), can be used to simplify these Boolean expressions.

Suppose we want to charge a higher shipping rate if we don't ship within the continental United States.

```
if (!(country == "USA"
    && state != "AK"
    && state != "HI"))
  shipping_charge = 20.00;
```

This test is a little bit complicated, and you have to think carefully through the logic. When it is not true that the country is USA and the state is not Alaska and the state is not Hawaii, then charge $20.00. Huh? It is not true that some people won't be confused by this code.

The computer doesn't care, but it takes human programmers to write and maintain the code. Therefore, it is useful to know how to simplify such a condition.

De Morgan's Law has two forms: one for the negation of an and expression and one for the negation of an or expression:

```
!(A && B)    is the same as    !A || !B
!(A || B)    is the same as    !A && !B
```

> De Morgan's law tells you how to negate && and || conditions.

Pay particular attention to the fact that the and and or operators are reversed by moving the not inward. For example, the negation of “the state is Alaska or it is Hawaii”,

```
!(state == "AK" || state == "HI")
```

is “the state is not Alaska and it is not Hawaii”:

```
!(state == "AK") && !(state == "HI")
```

## CHAPTER SUMMARY

### Use the `if` statement to implement a decision.

- The `if` statement allows a program to carry out different actions depending on the nature of the data to be processed.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_140_0.png)

### Implement comparisons of numbers and objects.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_140_1.png)

- Relational operators (`<`, `<=`, `>`, `>=`, `==`, `!=`) are used to compare numbers and strings.
- Lexicographic order is used to compare strings.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_140_2.png)

### Implement complex decisions that require multiple `if` statements.

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_140_3.png)

- Multiple alternatives are required for decisions that have more than two cases.
- When using multiple `if` statements, pay attention to the order of the conditions.

are necessary to actually understand the sentences. For example, consider the sentence “Last fall she enrolled in Michigan State”. The reader automatically realizes that “fall” is not related to falling down in this context, but refers to the season. While there is a state of Michigan, here Michigan State denotes the university. A priori, a computer program has none of this knowledge. The goal of the CYC project is to extract and store the requisite facts—that is, (1) people enroll in universities; (2) Michigan is a state; (3) many states have universities named X State University, often abbreviated as X State; (4) most people enroll in a university in the fall. By 1995, the project had codified about 100,000 common-sense concepts and about a million facts of knowledge relating them. Even this massive amount of data has not proven sufficient for useful applications.

In recent years, artificial intelligence technology has seen substantial advances. One of the most astounding examples is the outcome of a series of “grand challenges” for autonomous vehicles posed by the Defense Advanced Research Projects Agency (DARPA). Competitors were invited to submit a computer-controlled vehicle that had to complete an obstacle course without a human driver or remote control. The first event, in 2004, was a disappointment, with none of the entrants finishing the route. In 2005, five vehicles completed a grueling 212 km course in the Mojave desert. Stanford’s Stanley came in first, with an average speed of 30 km/h. In 2007, DARPA moved the competition to an “urban” environment, an abandoned air force base. Vehicles had to be able to interact with each other, following California traffic laws. As Stanford’s Sebastian Thrun explained:

![](img/6ec8c4bdbdda7d4ab1f2166b5332154c_140_4.png)

Winner of the 2007 DARPA Urban Challenge

> In the last Grand Challenge, it didn’t really matter whether an obstacle was a rock or a bush, because either way you’d just drive around it. The current challenge is to move from just sensing the environment to understanding the environment.
