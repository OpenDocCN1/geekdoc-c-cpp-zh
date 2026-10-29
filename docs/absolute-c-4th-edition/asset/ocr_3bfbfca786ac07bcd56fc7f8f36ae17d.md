```
**EXAMPLES**

```text
int count = 0, limit = 10, fudgeFactor = 2;
double distance = 999.99;
```
```

# **SYNTAX**

Alternative syntax for initializing in declarations:

```
```text
Type_Name Variable_Name_1 (Expression_for_Value_1),
             Variable_Name_2 (Expression_for_Value_2), ...;
```
```

# **EXAMPLES**

```
```text
int count(0), limit(10), fudgeFactor(2);
double distance(999.99);
```
```

# **Tip — USE MEANINGFUL NAMES**

Variable names and other names in a program should at least hint at the meaning or use of the thing they are naming. It is much easier to understand a program if the variables have meaningful names. Contrast

```
```text
x = y * z;
```
```

with the more suggestive

```
```text
distance = speed * time;
```
```

The two statements accomplish the same thing, but the second is easier to understand.

# ▪ **MORE ASSIGNMENT STATEMENTS**

A shorthand notation exists that combines the assignment operator (=) and an arithmetic operator so that a given variable can have its value changed by adding, subtracting, multiplying by, or dividing by a specified value. The general form is

```
```text
Variable Operator = Expression
```
```

which is equivalent to

```
```text
Variable = Variable Operator (Expression)
```
```