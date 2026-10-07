# Chapter 4

# Conditionals and recursion

# 4.1 The modulus operator

The modulus operator works on integers (and integer expressions) and yields the remainder when the first operand is divided by the second. In C++, the modulus operator is a percent sign, %. The syntax is exactly the same as for other operators:

```
int quotient = 7 / 3;
int remainder = 7 % 3;
```

The first operator, integer division, yields 2. The second operator yields 1. Thus, by 3 is 2 with 1 left over.

The modulus operator turns out to be surprisingly useful. For example, you can check whether one number is divisible by another: if x % y is zero, then x is divisible by y.

Also, you can use the modulus to extract the rightmost digit or digits from a number. For example, x % 10 yields the rightmost digit of x (in base 10). Similarly x % 100 yields the last two digits.

# 4.2 Conditional execution

In order to write useful programs, almost always need the ability to check certain conditions and change the behavior of the program accordingly. Conditional statements give us this ability. The simplest form is the if statement:

```
if (x > 0) {
    cout << "x is positive" << endl;
}
```

The expression in parentheses is called the condition. If it is true, then the statements in brackets get executed. If the condition is not true, nothing happens.