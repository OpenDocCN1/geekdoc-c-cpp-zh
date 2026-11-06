
## 2.2 Arithmetic

In the following sections, you will learn how to carry out arithmetic and mathematical calculations in C++.

### 2.2.1 Arithmetic Operators

![](img/23fb3582e93ebc95909e1de029c3d388_67_0.png)

C++ supports the same four basic arithmetic operations as a calculator—addition, subtraction, multiplication, and division—but it uses different symbols for multiplication and division.

You must write `a * b` to denote multiplication. Unlike in mathematics, you cannot write `a · b`, `a . b` or `a × b`. Similarly, division is always indicated with a `/`, never a `÷` or a fraction bar.

For example, `\frac{a+b}{2}` becomes `(a + b) / 2`.

Parentheses are used just as in algebra: to indicate in which order the subexpressions should be computed. For example, in the expression `(a + b) / 2`, the sum `a + b` is computed first, and then the sum is divided by 2. In contrast, in the expression

```text
a + b / 2
```

only `b` is divided by 2, and then the sum of `a` and `b / 2` is formed. Just as in regular algebraic notation, multiplication and division have a *higher precedence* than addition and subtraction. For example, in the expression `a + b / 2`, the `/` is carried out first, even though the `+` operation occurs further to the left. If both arguments of an arithmetic operation are integers, the result is an integer. If one or both arguments are floating-point numbers, the result is a floating-point number. For example, `4 * 0.5` is `2.0`.

> Use `*` for multiplication and `/` for division.

### 2.2.2 Increment and Decrement

Changing a variable by adding or subtracting 1 is so common that there is a special shorthand for it, namely

```cpp
counter++;
counter--;
```

The `++` increment operator gave the C++ programming language its name. C++ is the incremental improvement of the C language.

> The `++` operator adds 1 to a variable; the `--` operator subtracts 1.

### 2.2.3 Integer Division and Remainder

> If both arguments of `/` are integers, the remainder is discarded.

Division works as you would expect, as long as at least one of the numbers involved is a floating-point number. That is, `7.0 / 4.0`, `7 / 4.0`, and `7.0 / 4` all yield 1.75. However, if both numbers are integers, then the result of the division is always an integer, with the remainder discarded. That is,

```text
7 / 4
```

evaluates to 1 because 7 divided by 4 is 1 with a remainder of 3 (which is discarded). This can be a source of subtle programming errors—see Common Error 2.3 on page 43.

The `%` operator computes the remainder of an integer division.

If you are interested in the remainder only, use the `%` operator:

```text
7 % 4
```

is 3, the remainder of the integer division of 7 by 4. The `%` symbol has no analog in algebra. It was chosen because it looks similar to `/`, and the remainder operation is related to division. The operator is called *modulus*. (Some people call it *modulo* or *mod*.) It has no relationship with the percent operation that you find on some calculators.

Here is a typical use for the integer `/` and `%` operations. Suppose you have an amount of pennies in a piggybank:

```text
int pennies = 1729;
```

You want to determine the value in dollars and cents. You obtain the dollars through an integer division by 100.

```text
int dollars = pennies / 100;  // Sets dollars to 17
```

The integer division discards the remainder. To obtain the remainder, use the `%` operator:

```text
int cents = pennies % 100;  // Sets cents to 29
```

Another common use of the `%` operator is to check whether a number is even or odd. If a number n is even, then `n % 2` is zero.

![](img/23fb3582e93ebc95909e1de029c3d388_68_0.png)

### 2.2.4 Converting Floating-Point Numbers to Integers

Assigning a floating-point variable to an integer drops the fractional part.

When a floating-point value is assigned to an integer variable, the fractional part is discarded:

```text
double price = 2.55;
int dollars = price;  // Sets dollars to 2
```

Discarding the fractional part is not always what you want. Often, you want to round to the nearest integer. To round a positive floating-point value to the nearest integer, add 0.5 and then convert to an integer:

```text
int dollars = price + 0.5;  // Rounds to the nearest integer
```

In our example, adding 0.5 turns all values above 2.5 into values above 3. In particular, 2.55 is turned into 3.05, which is then truncated to 3. (For a negative floating-point value, you subtract 0.5.)

Because truncation is a potential cause for errors, your compiler may issue a warning that assigning a floating-point value to an integer variable is unsafe. See Special Topic 2.3 on page 46 on how to avoid this warning.

### 2.2.5 Powers and Roots

In C++, there are no symbols for powers and roots. To compute them, you must call *functions*. To take the square root of a number, you use the sqrt function. For example, √x is written as sqrt(x). To compute xⁿ, you write pow(x, n).

### Table 6 Other Mathematical Functions

| Function | Description |
| --- | --- |
| sin(x) | sine of x (x in radians) |
| cos(x) | cosine of x |
| tan(x) | tangent of x |
| log10(x) | (decimal log) log10(x), x > 0 |
| abs(x) | absolute value \|x\| |

Table 6 shows additional functions that are declared in the `<cmath>` header. Inputs and outputs are floating-point numbers.

### SELF CHECK

![](img/23fb3582e93ebc95909e1de029c3d388_70_0.png)

- 10. A bank account earns interest of p percent per year. In C++, how do you compute the interest earned in one year? Assume variables p and balance of type double have already been defined.
- 11. In C++, how do you compute the side length of a square whose area is stored in the variable area?
- 12. The volume of a sphere is given by V = 4/3 πr³.
      If the radius is given by a variable radius of type double, write a C++ expression for the volume. You may assume that π is defined by a constant PI.
- 13. What is the value of 1729 / 10 and 1729 % 10?
- 14. Suppose a punch recipe calls for a given amount of orange soda, measured in ounces.

      ```text
      int amount = 32;
      ```

      We can compute the number of 12-ounce cans needed, assuming that the amount does not evenly divide into 12:

      ```text
      int cans_needed = amount / 12 + 1;
      ```

      Use the `%` operator to determine how many ounces will be left over. For example, if 32 ounces are required, we need 3 cans and have 4 ounces left over.

![](img/23fb3582e93ebc95909e1de029c3d388_70_1.png)

### Practice It

Now you can try these exercises at the end of the chapter: R2.3, R2.5, P2.2.

### Common Error 2.3

**Unintended Integer Division**

![](img/23fb3582e93ebc95909e1de029c3d388_70_2.png)

It is unfortunate that C++ uses the same symbol, namely `/`, for both integer and floating-point division. These are really quite different operations. It is a common error to use integer division by accident. Consider this segment that computes the average of three integers:

```cpp
    cout << "Please enter your last three test scores: ";
    int s1;
    int s2;
    int s3;
    cin >> s1 >> s2 >> s3;
    double average = (s1 + s2 + s3) / 3; // Error
    cout << "Your average score is " << average << endl;
```

What could be wrong with that? Of course, the average of s1, s2, and s3 is

\(\frac{s1+s2+s3}{3}\)

Here, however, the `/` does not mean division in the mathematical sense. It denotes integer division because both s1 + s2 + s3 and 3 are integers. For example, if the scores add up to 14, the average is computed to be 4, the result of the integer division of 14 by 3. That integer 4 is then moved into the floating-point variable average. The remedy is to make the numerator or denominator into a floating-point number:

```cpp
double total = s1 + s2 + s3;
double average = total / 3;
```

or

```cpp
double average = (s1 + s2 + s3) / 3.0;
```

### Common Error 2.4

**Unbalanced Parentheses**

Consider the expression

`(-(b * b - 4 * a * c) / (2 * a)`

What is wrong with it? Count the parentheses. There are three `(` and two `)`. The parentheses are *unbalanced*. This kind of typing error is very common with complicated expressions. Now consider this expression.

`-(b * b - (4 * a * c))) / (2 * a`

This expression has three `(` and three `)`, but it still is not correct. In the middle of the expression,

`-(b * b - (4 * a * c))) / (2 * a`

there are only two `(` but three `)`, which is an error. In the middle of an expression, the count of `(` must be greater than or equal to the count of `)`, and at the end of the expression the two counts must be the same.

Here is a simple trick to make the counting easier without using pencil and paper. It is difficult for the brain to keep two counts simultaneously. Keep only one count when scanning the expression. Start with 1 at the first opening parenthesis, add 1 whenever you see an opening parenthesis, and subtract one whenever you see a closing parenthesis. Say the numbers aloud as you scan the expression. If the count ever drops below zero, or is not zero at the end, the parentheses are unbalanced. For example, when scanning the previous expression, you would mutter

```text
-(b * b - (4 * a * c))) / (2 * a
 1       2             1 0 -1
```

and you would find the error.

![](img/23fb3582e93ebc95909e1de029c3d388_71_0.png)
