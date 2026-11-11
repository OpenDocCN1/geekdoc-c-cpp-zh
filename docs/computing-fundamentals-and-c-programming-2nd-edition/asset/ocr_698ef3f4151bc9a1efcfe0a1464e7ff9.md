significant digits permissible, the final value is an approximation of the correct result. If **x**, **y**, and **z** are **floats**, then we will have:

```
```
x = 6.0/7.0 = 0.857143
y = 1.0/3.0 = 0.333333
z = -2.0/3.0 = -0.666667
```
```

The operator % cannot be used with real operands.

# ### 5.2.3 Mixed-mode Arithmetic

When one of the operands is real and the other is integer, the expression is called a *mixed-mode arithmetic expression*. If either operand is of the real type, then only the real operation is performed and the result is always a real number. Thus

```
```
15/10.0 = 1.5
```
```

whereas

```
```
15/10 = 1
```
```

More about mixed operations will be discussed later when we deal with the evaluation of expressions.

# ### 5.3 RELATIONAL OPERATORS

**LO 5.1**

We often compare two quantities and depending on their relation, take certain decisions. For example, we may compare the age of two persons, or the price of two items, and so on. These comparisons can be done with the help of *relational operators*. We have already used the symbol '<', meaning 'less than'. An expression such as

```
```
a < b or 1 < 20
```
```

containing a relational operator is termed as a *relational expression*. The value of a relational expression is either *one* or *zero*. It is *one* if the specified relation is *true* and *zero* if the relation is *false*. For example

```
```
10 < 20 is true
```
```

but

```
```
20 < 10 is false
```
```

C supports six relational operators in all. These operators and their meanings are shown in Table 5.2.

**Table 5.2** *Relational Operators*

| Operator | Meaning |
| --- | --- |
| `<` | is less than |
| `<=` | is less than or equal to |
| `>` | is greater than |
| `>=` | is greater than or equal to |
| `==` | is equal to |
| `!=` | is not equal to |

A simple relational expression contains only one relational operator and takes the following form:

*ae-1 relational operator ae-2*