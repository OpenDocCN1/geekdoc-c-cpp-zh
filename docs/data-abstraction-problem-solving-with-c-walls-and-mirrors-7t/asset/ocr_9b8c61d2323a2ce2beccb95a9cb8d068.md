To convert this expression to prefix form, you first move each operator to the position marked by its corresponding open parenthesis:

```
((a b)c)
↓ ↓
↑ +
```

Converting to prefix form

Next, you remove the parentheses to get the desired prefix expression:

```
* + a b
```

Similarly, to convert the infix expression to postfix form, you move each operator to the position marked by its corresponding close parenthesis:

Converting to postfix form

```
((ab)c)
↓ ↓
↑ *
```

Then you remove the parentheses:

```
a b + c *
```

When an infix expression is not fully parenthesized, these conversions are more complex. Chapter 6 discusses the general case of converting an infix expression to postfix form.

The advantage of prefix and postfix expressions is that they never need precedence rules, association rules, or parentheses. Therefore, the grammars for prefix and postfix expressions are quite simple. In addition, the algorithms that recognize and evaluate these expressions are relatively straightforward.

Prefix and postfix expressions never need precedence rules, association rules, or parentheses

# 5.2.2 Prefix Expressions

A grammar that defines the language of all prefix expressions is

```
<prefix> = <identifier> | <operator> <prefix> <prefix>
<operator> = + | - | * | /
<identifier> = a | b | ... | z
```

From this grammar, you can construct a recursive algorithm that recognizes whether a string is a prefix expression. If the string is of length 1, it is a prefix expression if and only if the string is a single lowercase letter. Strings of length 1 can be base case. If the length of the string is greater than 1, then for it to be a legal prefix expression, it must be of the form

```
<operator> <prefix> <prefix>
```

Thus, the algorithm must check to see whether

+   The first character of the string is an operator

and

+   The remainder of the string consists of two consecutive prefix expressions

The first task is trivial, but the second is a bit tricky. How can you tell whether you are looking at two consecutive prefix expressions? A key observation is that if you add any string of nonblank characters to the end of a prefix expression, you will no longer have a prefix expression. That is, if E is